---
seo-title: Tracking heruntergeladener Inhalte
title: Tracking heruntergeladener Inhalte
uuid: 7186689 d -9602-4 e 3 f -833 c -8297 aae 1 d 009
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# Tracking heruntergeladener Inhalte{#track-downloaded-content}

## Überblick {#section_hcy_3pk_cfb}

Die Funktion zum Herunterladen von Inhalten bietet die Möglichkeit, Medienkonsum zu verfolgen, während ein Benutzer offline ist. Beispielsweise lädt ein Anwender eine App herunter und installiert sie auf einem Mobilgerät. Der Anwender lädt dann mit der App Inhalte in den lokalen Speicher auf dem Gerät herunter. Um diese heruntergeladenen Daten zu verfolgen, hat Adobe die Funktion Heruntergeladene Inhalte entwickelt. Wenn der Benutzer mit dieser Funktion Inhalte aus dem Speicher eines Geräts abspielt, werden Verfolgungsdaten auf dem Gerät gespeichert, unabhängig von der Verbindung des Geräts. Wenn der Benutzer die Wiedergabesitzung beendet und das Gerät online zurückkehrt, werden die gespeicherten Verfolgungsinformationen an die Mediensammlung-API innerhalb einer einzelnen Payload gesendet. Von dort fließen die Verarbeitung und die Berichterstellung in der Mediensammlung-API als normal.

Vergleichen Sie die beiden Ansätze:

* Online

   Mit diesem Echtzeitansatz sendet der Medienplayer Verfolgungsdaten bei jedem Player-Ereignis und sendet alle zehn Sekunden Netzwerkpings (alle eine Sekunde für Anzeigen), eine um eins bis ein Backend.

* Offline (Funktion für heruntergeladene Inhalte)

   Bei diesem Batch-Verarbeitungsansatz müssen dieselben Sitzungsereignisse generiert werden, sie werden jedoch auf dem Gerät gespeichert, bis sie als einzelne Sitzung an das Back-End gesendet werden (siehe Beispiel unten).

Jeder Ansatz bietet seine Vor- und Nachteile:
* Das Online-Szenario verfolgt die Echtzeit-Verfolgung; Hierfür muss vor jedem Netzwerkaufruf eine Verbindungsprüfung erfolgen.
* Das Offline-Szenario (Funktion für heruntergeladene Inhalte) benötigt nur eine Netzwerkverbindung, erfordert jedoch auch einen größeren Speicherbedarf auf dem Gerät.

## Implementierung {#section_jhp_jpk_cfb}

### Ereignisschemata

Die Funktion "Heruntergeladene Inhalte" ist einfach die Offline-Version der Online-Mediensammlung-API (Standard). Daher müssen die Ereignisdaten, die die Player-Stapel verwenden, dieselben Ereignisschemata verwenden, die Sie beim Tätigen von Online-Aufrufen verwenden. Informationen zu diesen Schemata finden Sie unter:
* [Übersicht;](/help/media-collection-api/mc-api-overview.md)
* [Validieren von Ereignisanfragen](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Reihenfolge der Ereignisse

* Das erste Ereignis in der Batch-Nutzlast muss für die Mediensammlung-API `sessionStart` wie üblich lauten.
* **Sie`media.downloaded: true`** müssen in den Standard-Metadatenparametern (`params` Schlüssel) des `sessionStart` Ereignisses enthalten sein, um das Backend anzugeben, dass Sie heruntergeladene Inhalte senden. Wenn dieser Parameter beim Senden heruntergeladener Daten nicht oder auf false festgelegt ist, gibt die API einen 400-Antwortcode zurück (ungültige Anforderung). Dieser Parameter unterscheidet heruntergeladene und live-Inhalte in das Back-End. (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* Es liegt an einer korrekten Implementierung, Abspielereignisse in der Reihenfolge ihres Auftretens richtig zu speichern.

### Antwortcodes

* 201 - Created: Successful Request; die Daten sind gültig und die Sitzung wurde erstellt und wird verarbeitet.
* 400 - Bad Request; die Schemavalidierung ist fehlgeschlagen, alle Daten werden verworfen, es werden keine Sitzungsdaten verarbeitet.

## Integration mit Adobe Analtyics {#section_cty_kpk_cfb}

Bei der Berechnung der Analytics-Start-/Close-Aufrufe für das heruntergeladene Inhaltsszenario stellt das Back-End ein zusätzliches Analytics-Feld dar, das die `ts.` Zeitstempel für die ersten und letzten empfangenen Ereignisse darstellt (starten und abschließen). Mit diesem Mechanismus kann eine abgeschlossene Mediensitzung am richtigen Zeitpunkt platziert werden (d. h., auch wenn der Benutzer mehrere Tage nicht online ist, wird die Mediensitzung zu dem Zeitpunkt aufgezeichnet, zu dem der Inhalt tatsächlich angezeigt wurde). Sie müssen dieses Verfahren auf der Seite von Adobe Analytics aktivieren, indem Sie einen _optionalen Zeitstempel für die Report Suite erstellen._ Informationen zum Aktivieren eines optionalen Zeitstempel für die Report Suite finden Sie unter [Optionale Zeitstempel.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Vergleich von Beispielsitzungen {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### Online-Inhalt

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

### Heruntergeladener Inhalt

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

