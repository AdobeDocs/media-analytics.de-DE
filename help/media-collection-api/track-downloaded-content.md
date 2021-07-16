---
title: Tracking heruntergeladener Inhalte
description: Erfahren Sie, wie Sie mit der Funktion für heruntergeladene Inhalte den Medienkonsum verfolgen können, wenn ein Benutzer offline ist.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 100%

---

# Tracking heruntergeladener Inhalte{#track-downloaded-content}

## Überblick {#overview}

Die Funktion für heruntergeladene Inhalte bietet die Möglichkeit, die Mediennutzung zu verfolgen, während ein Benutzer offline ist. Ein Benutzer lädt beispielsweise eine Mobile App auf ein Mobilgerät herunter und installiert sie, um dann mit der Mobile App Inhalte in die lokale Datenspeicherung auf dem Gerät herunterzuladen. Um das Tracking der heruntergeladenen Daten zu ermöglichen, hat Adobe eine Funktion für heruntergeladene Inhalte entwickelt. Mit dieser Funktion werden Tracking-Daten unabhängig von der Konnektivität des Geräts gespeichert, wenn der Benutzer Inhalte aus dem Speicher des Geräts wiedergibt. Wenn der Benutzer die Wiedergabesitzung beendet hat und das Gerät wieder online ist, werden die gespeicherten Tracking-Informationen in einer einzelnen Payload an das Backend der Media Collection API gesendet. Die gespeicherten Tracking-Informationen werden dann wie gewohnt in der Media Collection API verarbeitet und für Berichte verwendet.

Vergleichen Sie die beiden Ansätze:

* Online

   Bei diesem Echtzeit-Ansatz sendet der Medienplayer Tracking-Daten für jedes Player-Ereignis. Außerdem sendet er alle zehn Sekunden (bei Anzeigen jede Sekunde) jeweils einen einzelnen Netzwerk-Ping an das Backend.

* Offline (Funktion für heruntergeladene Inhalte)

   Bei diesem Ansatz der Stapelverarbeitung müssen dieselben Sitzungsereignisse generiert werden, die jedoch auf dem Gerät gespeichert werden, bis sie als einzelne Sitzung an das Backend gesendet werden (siehe Beispiel unten).

Jeder Ansatz hat seine Vor- und Nachteile:
* Das Online-Szenario verfolgt in Echtzeit. Dies erfordert eine Konnektivitätsprüfung vor jedem Netzwerkaufruf.
* Für das Offline-Szenario (Funktion für heruntergeladene Inhalte) ist nur eine Prüfung der Netzwerkverbindung erforderlich, es ist jedoch ein größerer Speicherbedarf auf dem Gerät erforderlich.

## Implementierung {#implementation}

### Unterstützte Plattformen

Das Inhalts-Tracking wird auf mobilen iOS- und Android-Geräten unterstützt.

### Ereignisschemas

Bei der Funktion für heruntergeladene Inhalte handelt es sich um die Offline-Version der (standardmäßigen) Online-Media Collection API. Daher müssen die Ereignisdaten, die Ihr Player stapelt und an das Backend sendet, dieselben Ereignisschemas verwenden, die Sie auch bei Online-Aufrufen verwenden. Informationen zu diesen Schemas finden Sie unter:
* [Überblick;](/help/media-collection-api/mc-api-overview.md)
* [Validieren von Ereignisanfragen](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Reihenfolge der Ereignisse

* Das erste Ereignis in der Stapel-Nutzlast muss wie bei der Media Collection API üblich `sessionStart` sein.
* **Sie müssen `media.downloaded: true`** in die Standard-Metadatenparameter (`params`-Schlüssel) für das Ereignis `sessionStart` einschließen, um dem Backend anzuzeigen, dass Sie heruntergeladene Inhalte senden. Wenn dieser Parameter nicht vorhanden ist oder auf „false“ (falsch) gesetzt ist, wenn Sie heruntergeladene Daten senden, antwortet die API mit dem Antwortcode 400 („Bad Request“ (ungültige Anforderung)). Dieser Parameter unterscheidet zwischen heruntergeladenen und Live-Inhalten im Backend. Wenn `media.downloaded: true` auf eine Live-Sitzung eingestellt ist, wird dies ebenfalls zu einer Antwort mit dem Code 400 von der API führen.
* Es liegt an einer korrekten Implementierung, Abspielereignisse in der Reihenfolge ihres Auftretens richtig zu speichern.

### Antwortcodes

* 201 - Erstellt: die Anfrage ist erfolgreich; die Daten sind gültig und die Sitzung wurde erstellt wurde und wird verarbeitet.
* 400 - Ungültige Anfrage; die Validierung des Schemas ist fehlgeschlagen, alle Daten werden verworfen, keine Sitzungsdaten werden verarbeitet.

## Integration mit Adobe Analytics {#integration-with-adobe-analtyics}

Bei der Berechnung der Analytics-Start-/Schließen-Aufrufe für das Szenario mit heruntergeladenen Inhalten verwendet das Backend ein zusätzliches Analytics-Feld `ts.` Dabei handelt es sich um Zeitstempel für das erste und letzte empfangene Ereignis (Start und Abschluss). Dieses Verfahren ermöglicht es, eine abgeschlossene Mediensitzung am richtigen Zeitpunkt zu platzieren (d. h., selbst wenn der Benutzer mehrere Tage lang nicht online war, erfährt er, dass die Mediensitzung zum Zeitpunkt der tatsächlichen Betrachtung des Inhalts stattgefunden hat). Sie müssen dieses Verfahren auf der Seite von Adobe Analytics aktivieren, indem Sie einen _optionalen Zeitstempel für die Report Suite erstellen._ Informationen zum Aktivieren eines optionalen Zeitstempel für die Report Suite finden Sie unter [Optionale Zeitstempel.](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=de)

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
