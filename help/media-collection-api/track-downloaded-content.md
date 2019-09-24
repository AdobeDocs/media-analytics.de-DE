---
seo-title: Tracking heruntergeladener Inhalte
title: Tracking heruntergeladener Inhalte
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# Tracking heruntergeladener Inhalte{#track-downloaded-content}

## Überblick {#section_hcy_3pk_cfb}

Die Funktion "Heruntergeladene Inhalte"bietet die Möglichkeit, den Medienkonsum zu verfolgen, während ein Benutzer offline ist. Beispielsweise lädt ein Anwender eine App herunter und installiert sie auf einem Mobilgerät. Der Anwender lädt dann mit der App Inhalte in den lokalen Speicher auf dem Gerät herunter. Um diese heruntergeladenen Daten zu verfolgen, hat Adobe die Funktion für heruntergeladene Inhalte entwickelt. Mit dieser Funktion werden beim Abspielen von Inhalten aus dem Speicher eines Geräts Verfolgungsdaten auf dem Gerät gespeichert, unabhängig von der Konnektivität des Geräts. Wenn der Benutzer die Wiedergabesitzung beendet und das Gerät online zurückgibt, werden die gespeicherten Verfolgungsinformationen innerhalb einer einzigen Nutzlast an das Media Collection API-Back-End gesendet. Von dort erfolgt die Verarbeitung und Berichterstellung wie gewohnt in der Medienerfassungs-API.

Vergleichen Sie die beiden Ansätze:

* Online

   Bei diesem Echtzeitansatz sendet der Medienplayer bei jedem Player-Ereignis Verfolgungsdaten und sendet alle zehn Sekunden (bei Anzeigen alle eine Sekunde) Netzwerkpings nacheinander an das Backend.

* Offline (Funktion für heruntergeladene Inhalte)

   Bei diesem Verfahren der Stapelverarbeitung müssen dieselben Sitzungsereignisse generiert werden, sie werden jedoch auf dem Gerät gespeichert, bis sie als einzelne Sitzung an das Back-End gesendet werden (siehe Beispiel unten).

Jeder Ansatz hat seine Vor- und Nachteile:
* Das Online-Szenario verfolgt sich in Echtzeit. dies erfordert eine Verbindungsprüfung vor jedem Netzwerkaufruf.
* Für das Offline-Szenario (Funktion für heruntergeladene Inhalte) ist nur eine Prüfung der Netzwerkverbindung erforderlich, es ist jedoch auch ein größerer Speicherbedarf auf dem Gerät erforderlich.

## Implementierung {#section_jhp_jpk_cfb}

### Ereignisschemata

Bei der Funktion für heruntergeladene Inhalte handelt es sich lediglich um die Offline-Version der (Standard-)Online-Medienerfassungs-API. Daher müssen die Ereignisdaten, die Ihr Player stapelt und an das Back-End sendet, dieselben Ereignisschemata verwenden, die Sie auch bei Online-Aufrufen verwenden. Informationen zu diesen Schemata finden Sie unter:
* [Übersicht;](/help/media-collection-api/mc-api-overview.md)
* [Validieren von Ereignisanfragen](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Reihenfolge der Ereignisse

* Das erste Ereignis in der Batch-Nutzlast muss mit der Media Collection-API wie gewohnt `sessionStart` sein.
* **Sie müssen`media.downloaded: true`** in die Standard-Metadatenparameter (`params` `sessionStart` -Schlüssel) für das Ereignis einschließen, um dem Back-End anzuzeigen, dass Sie heruntergeladene Inhalte senden. Wenn dieser Parameter beim Senden von heruntergeladenen Daten nicht vorhanden ist oder auf "false"gesetzt ist, gibt die API einen 400-Antwortcode (Ungültige Anforderung) zurück. Dieser Parameter unterscheidet heruntergeladene und Live-Inhalte bis zum Back-End. (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* Es liegt an einer korrekten Implementierung, Abspielereignisse in der Reihenfolge ihres Auftretens richtig zu speichern.

### Antwortcodes

* 201 - Created: Successful Request; die Daten sind gültig und die Sitzung wurde erstellt und wird verarbeitet.
* 400 - Bad Request; die Schemavalidierung ist fehlgeschlagen, alle Daten werden verworfen, es werden keine Sitzungsdaten verarbeitet.

## Integration mit Adobe Analtyics {#section_cty_kpk_cfb}

Bei der Berechnung der Analytics-Start-/Schließen-Aufrufe für das heruntergeladene Inhaltsszenario legt das Back-End ein zusätzliches Analytics-Feld namens `ts.` "Diese Zeitstempel sind für das erste und letzte empfangene Ereignis (Start und Abschluss) fest. Auf diese Weise kann eine abgeschlossene Mediensitzung zum richtigen Zeitpunkt platziert werden (d. h., selbst wenn der Benutzer mehrere Tage lang nicht wieder online ist, wird berichtet, dass die Mediensitzung zum Zeitpunkt der tatsächlichen Anzeige stattgefunden hat). Sie müssen dieses Verfahren auf der Seite von Adobe Analytics aktivieren, indem Sie einen _optionalen Zeitstempel für die Report Suite erstellen._ Informationen zum Aktivieren eines optionalen Zeitstempel für die Report Suite finden Sie unter [Optionale Zeitstempel.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Vergleich von Beispielsitzungen {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### Online-Inhalte

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### Heruntergeladene Inhalte

```
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

