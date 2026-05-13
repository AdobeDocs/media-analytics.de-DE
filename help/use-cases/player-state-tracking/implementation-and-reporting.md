---
title: Implementierung und Reporting
description: Erfahren Sie, wie Sie die Player-Status-Tracking-Funktion implementieren einschließlich
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NzekVHZYctiEjAWDpRhIdiw74amAX3wTX-z2nZDgvIw
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
  - id: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 76%

---

# Implementierung und Reporting

Während einer Wiedergabesitzung muss jedes Statusereignis (vom Beginn bis zum Ende) einzeln getrackt werden. Die Media SDK und die Mediensammlungs-API stellen Tracking-Methoden für diese Funktion bereit.

Media SDK umfasst zwei Methoden zur benutzerdefinierten Statusverfolgung:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Die Mediensammlungs-API enthält zwei Ereignisse, die `media.stateName` als erforderlichen Parameter aufweisen:

`stateStart` und `stateEnd`

## Implementierung des Medien-SDK

Player-Status beginnt

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Player-Status endet

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Implementierung der Mediensammlungs-API

Player-Status beginnt

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

Player-Status endet

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## Statusmetriken

Die für die einzelnen Status bereitgestellten Metriken werden berechnet, als Kontextdatenparameter an Adobe Analytics gesendet und für das Reporting gespeichert. Für jeden Status stehen drei Metriken zur Verfügung:

* `a.media.states.[state.name].set = true` – ist auf „true“ gesetzt, wenn der Status für jede einzelne Wiedergabe eines Streams mindestens einmal festgelegt wurde.
* `a.media.states.[state.name].count = 4` – Identifiziert die Anzahl der Vorkommnisse eines Status während jeder einzelnen Wiedergabe eines Streams
* `a.media.states.[state.name].time = 240` – Identifiziert die Gesamtstatusdauer in Sekunden für jede einzelne Wiedergabe eines Streams

## Reporting

Alle Player-Statusmetriken können für jede in Analysis Workspace verfügbare Visualisierung von Berichten oder für eine Komponente (Segment, berechnete Metriken) verwendet werden, sobald eine Report Suite für das Player-Status-Tracking aktiviert wurde. Diese Metriken können über die Admin Console für jeden einzelnen Bericht mithilfe der Einrichtung der Medienberichte (Einstellungen bearbeiten > Medienverwaltung > Medienberichte) aktiviert werden.

![](assets/report-setup.png)

In Analysis Workspace befinden sich alle neuen Eigenschaften im Bedienfeld Metriken . Sie können beispielsweise nach `full screen` suchen, um die Vollbilddaten im Metrikbedienfeld anzuzeigen.

![](assets/full-screen-report.png)

## Importieren der vom Player angegebenen Metriken in Adobe Experience Platform

In Analytics gespeicherte Daten können für jeden Zweck verwendet werden. Die Player-Statusmetriken können mithilfe von XDM in Adobe Experience Platform importiert und mit Customer Journey Analytics verwendet werden. Die Standardstatuseigenschaften haben bestimmte Eigenschaften, während die benutzerdefinierten Statuseigenschaften über die benutzerdefinierten Ereignisse verfügbar sind.
