---
title: Tracking heruntergeladener Inhalte
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: be68a7abf7d5fd4cc725b040583801f2308ab066
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 56%

---


# Tracking heruntergeladener Inhalte {#track-downloaded-content}

## Überblick {#overview}

Die Funktion für heruntergeladene Inhalte bietet die Möglichkeit, die Mediennutzung zu verfolgen, während ein Benutzer offline ist. Ein Benutzer lädt beispielsweise eine App auf ein Mobilgerät herunter und installiert sie, um dann mit der App Inhalte in die lokale Datenspeicherung auf dem Gerät herunterzuladen. Um die heruntergeladenen Daten zu verfolgen, hat Adobe die Funktion für heruntergeladene Inhalte entwickelt. Mit dieser Funktion werden beim Abspielen von Inhalten aus der Datenspeicherung des Geräts Verfolgungsdaten auf dem Gerät gespeichert, unabhängig von der Geräteverbindung. Wenn der Benutzer die Wiedergabesitzung beendet und das Gerät online zurückgibt, werden die gespeicherten Verfolgungsinformationen innerhalb einer einzigen Nutzlast an das Media Collection API-Back-End gesendet. Die gespeicherten Verfolgungsinformationen werden dann wie gewohnt in der Media Collection-API verarbeitet und gemeldet.

Vergleichen Sie die beiden Ansätze:

* Online

   Bei diesem Echtzeitansatz sendet der Medienplayer Verfolgungsdaten für jedes Player-Ereignis und sendet alle zehn Sekunden (bei Anzeigen alle eine Sekunde) Netzwerkpings nacheinander an das Back-End.

* Offline (Funktion für heruntergeladene Inhalte)

   Bei diesem Verfahren der Stapelverarbeitung müssen dieselben Sitzungs-Ereignis generiert werden, sie werden jedoch auf dem Gerät gespeichert, bis sie als Einzelsitzung an das Back-End gesendet werden (siehe Beispiel unten).

Jeder Ansatz hat seine Vor- und Nachteile:
* Das Online-Szenario verfolgt in Echtzeit. Dies erfordert eine Konnektivitätsprüfung vor jedem Netzwerkaufruf.
* Für das Offline-Szenario (Funktion für heruntergeladene Inhalte) ist nur eine Prüfung der Netzwerkverbindung erforderlich, es ist jedoch ein größerer Speicherbedarf auf dem Gerät erforderlich.

## Implementierung {#implementation}

### Unterstützte Plattformen

Die Inhaltsverfolgung wird auf mobilen iOS- und Android-Geräten unterstützt.

### Ereignisschemas

Die Funktion &quot;Heruntergeladene Inhalte&quot;ist die Offlineversion der (Standard-)Online-Medienerfassungs-API. Daher müssen die Ereignis-Daten, die Ihr Player stapelt und an das Back-End sendet, dieselben Ereignis-Schema verwenden, die Sie beim Aufrufen über das Internet verwenden. Informationen zu diesen Schemas finden Sie unter:
* [Überblick;](/help/media-collection-api/mc-api-overview.md)
* [Validieren von Ereignisanfragen](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Reihenfolge der Ereignisse

* Das erste Ereignis in der Stapel-Nutzlast muss wie bei der Media Collection API üblich `sessionStart` sein.
* **Sie müssen`media.downloaded: true`** in die Standard-Metadatenparameter (`params``sessionStart`-Schlüssel) für das Ereignis einschließen, um dem Backend anzuzeigen, dass Sie heruntergeladene Inhalte senden. Wenn dieser Parameter nicht vorhanden ist oder auf „false“ (falsch) gesetzt ist, wenn Sie heruntergeladene Daten senden, antwortet die API mit dem Antwortcode 400 („Bad Request“ (ungültige Anforderung)). Dieser Parameter unterscheidet zwischen heruntergeladenen und Live-Inhalten im Backend. If`media.downloaded: true`is set on a live session, this will likewise result in a 400 response from the API.
* Es liegt an einer korrekten Implementierung, Abspielereignisse in der Reihenfolge ihres Auftretens richtig zu speichern.

### Antwortcodes

* 201 - Erstellt: die Anfrage ist erfolgreich; die Daten sind gültig und die Sitzung wurde erstellt wurde und wird verarbeitet.
* 400 - Ungültige Anfrage; die Validierung des Schemas ist fehlgeschlagen, alle Daten werden verworfen, keine Sitzungsdaten werden verarbeitet.

## Integration mit Adobe Analtyics {#integration-with-adobe-analtyics}

Bei der Berechnung der Analytics-Start-/Schließen-Aufrufe für das Szenario mit heruntergeladenen Inhalten verwendet das Backend ein zusätzliches Analytics-Feld `ts.`. Dabei handelt es sich um Zeitstempel für das erste und letzte empfangene Ereignis (Start und Abschluss). Dieses Verfahren ermöglicht es, eine abgeschlossene Mediensitzung am richtigen Zeitpunkt zu platzieren (d. h., selbst wenn der Benutzer mehrere Tage lang nicht online war, erfährt er, dass die Mediensitzung zum Zeitpunkt der tatsächlichen Betrachtung des Inhalts stattgefunden hat). Sie müssen dieses Verfahren auf der Seite von Adobe Analytics aktivieren, indem Sie einen _optionalen Zeitstempel für die Report Suite erstellen._ Informationen zum Aktivieren eines optionalen Zeitstempel für die Report Suite finden Sie unter [Optionale Zeitstempel.](https://docs.adobe.com/content/help/de-DE/analytics/admin/admin-tools/timestamp-optional.html)

## Vergleich von Beispielsitzungen {#sample-session-comparison}

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

## Media-Tracker-API-Referenz

Informationen zum Konfigurieren von heruntergeladenen Inhalten finden Sie in der [Media Tracker API-Referenz](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference).
