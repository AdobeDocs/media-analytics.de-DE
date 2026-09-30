---
title: Tracking von offline heruntergeladenen Inhalten in Streaming-Medien-Services
description: Erfahren Sie, wie Sie mit der Funktion für heruntergeladene Inhalte den Medienkonsum verfolgen können, wenn ein Benutzer offline ist.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Streaming Media
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/rtLBRcyLB8D8HPBj-Qw5LD824Fu8KeUDsLokJCn2Wfc'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: e992d880-33bc-4949-a648-aa7d410276cd
    internal-label: Validation
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 91%
---
# Tracking heruntergeladener Inhalte{#track-downloaded-content}

## Überblick {#overview}

Die Funktion für heruntergeladene Inhalte bietet die Möglichkeit, die Mediennutzung zu verfolgen, während ein Benutzer offline ist. Ein Benutzer lädt beispielsweise eine Mobile App auf ein Mobilgerät herunter und installiert sie, um dann mit der Mobile App Inhalte in die lokale Datenspeicherung auf dem Gerät herunterzuladen. Um das Tracking der heruntergeladenen Daten zu ermöglichen, hat Adobe die Funktion „Heruntergeladener Inhalt“ entwickelt. Mit dieser Funktion werden Tracking-Daten unabhängig von der Konnektivität des Geräts gespeichert, wenn der Benutzer Inhalte aus dem Speicher des Geräts wiedergibt. Wenn der Benutzer die Wiedergabesitzung beendet hat und das Gerät wieder online ist, werden die gespeicherten Tracking-Informationen in einer einzelnen Payload an das Backend der Media Collection API gesendet. Die gespeicherten Tracking-Informationen werden dann wie gewohnt in der Media Collection API verarbeitet und für Berichte verwendet.

Vergleichen Sie die beiden Ansätze:

* Online

  Bei diesem Echtzeit-Ansatz sendet der Medienplayer Tracking-Daten für jedes Player-Ereignis. Außerdem sendet er alle zehn Sekunden (bei Anzeigen jede Sekunde) jeweils einen einzelnen Netzwerk-Ping an das Backend.

* Offline (Funktion „Heruntergeladener Inhalt“)

  Bei diesem Ansatz der Stapelverarbeitung müssen dieselben Sitzungsereignisse generiert werden, die jedoch auf dem Gerät gespeichert werden, bis sie als einzelne Sitzung an das Backend gesendet werden (siehe Beispiel unten).

Jeder Ansatz hat seine Vor- und Nachteile:
* Das Online-Szenario verfolgt in Echtzeit. Dies erfordert eine Konnektivitätsprüfung vor jedem Netzwerkaufruf.
* Für das Offline-Szenario (Funktion für heruntergeladene Inhalte) ist nur eine Prüfung der Netzwerkverbindung erforderlich, es ist jedoch ein größerer Speicherbedarf auf dem Gerät erforderlich.

## Implementierung {#implementation}

### Unterstützte Plattformen

Das Inhalts-Tracking wird auf iOS- und Android-Mobilgeräten unterstützt.

### Ereignisschemas

Die Funktion für heruntergeladenen Inhalt ist die Offline-Version der (standardmäßigen) Online-Media-Collection-API. Daher müssen die Ereignisdaten, die Ihr Player bündelt und an das Backend sendet, dieselben Ereignis-Schemata verwenden, die Sie auch bei Online-Aufrufen verwenden. Informationen zu diesen Schemas finden Sie unter:
* [Überblick;](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/)
* [Validieren von Ereignisanfragen](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/implementation)

### Reihenfolge der Ereignisse

* Das erste Ereignis in der Stapel-Nutzlast muss wie bei der Media Collection API üblich `sessionStart` sein.
* **Sie müssen `media.downloaded: true`** in die Standard-Metadatenparameter (`params`-Schlüssel) für das Ereignis `sessionStart` einschließen, um dem Backend anzuzeigen, dass Sie heruntergeladene Inhalte senden. Wenn dieser Parameter nicht vorhanden ist oder auf „false“ (falsch) gesetzt ist, wenn Sie heruntergeladene Daten senden, antwortet die API mit dem Antwortcode 400 („Bad Request“ (ungültige Anforderung)). Dieser Parameter unterscheidet zwischen heruntergeladenem und Live Content im Backend. Wenn `media.downloaded: true` auf eine Live-Sitzung eingestellt ist, wird dies ebenfalls zu einer Antwort mit dem Code 400 von der API führen.
* Es liegt an einer korrekten Implementierung, Abspielereignisse in der Reihenfolge ihres Auftretens richtig zu speichern.

### Antwortcodes

* 201 – Erstellt: Die Anfrage war erfolgreich; die Daten sind gültig und die Sitzung wurde erstellt und wird verarbeitet.
* 400 – Ungültige Anfrage; die Schemavalidierung ist fehlgeschlagen, alle Daten werden verworfen, keine Sitzungsdaten werden verarbeitet.

## Integration mit Adobe Analytics {#integration-with-adobe-analtyics}

Bei der Berechnung der Analytics-Start-/Schließen-Aufrufe für das Szenario mit heruntergeladenen Inhalten verwendet das Backend ein zusätzliches Analytics-Feld `ts.` Dabei handelt es sich um Zeitstempel für das erste und letzte empfangene Ereignis (Start und Abschluss). Dieses Verfahren ermöglicht es, eine abgeschlossene Mediensitzung am richtigen Zeitpunkt zu platzieren (d. h., selbst wenn der Benutzer mehrere Tage lang nicht online war, erfährt er, dass die Mediensitzung zum Zeitpunkt der tatsächlichen Betrachtung des Inhalts stattgefunden hat). Sie müssen diesen Mechanismus auf der Adobe Analytics-Seite aktivieren, indem Sie eine _optionale Report Suite mit Zeitstempel“ erstellen_ Informationen zum Aktivieren eines Zeitstempels für eine optionale Report Suite finden Sie unter [Zeitstempel optional.](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=de)

## Vergleich von Beispielsitzungen {#sample-session-comparison}

### Online-Inhalte

```
POST /api/v1/sessions HTTP/1.1

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
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### Hinweis zu veralteten Versionen

>[!IMPORTANT]
>
>Heruntergeladene Inhalte konnten zuvor auch an die `/api/v1/sessions`-API gesendet werden. Diese Methode zum Tracking heruntergeladener Inhalte ist **veraltet** und wird in Zukunft **entfernt**.


Die `/api/v1/sessions`-API akzeptiert nur Sitzungsinitialisierungs-Ereignisse.
Bei Verwendung der neuen API ist die zuvor obligatorische `media.downloaded`-Markierung nicht mehr erforderlich.
Wir empfehlen dringend die Verwendung der `/api/v1/downloaded`-API für neue heruntergeladene Inhaltsimplementierungen sowie die Aktualisierung vorhandener Implementierungen, die auf der alten API basieren.


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

## Medien-Tracker-API-Referenz

Informationen zum Konfigurieren von heruntergeladenen Inhalten finden Sie in der [Media Tracker API-Referenz](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/).
