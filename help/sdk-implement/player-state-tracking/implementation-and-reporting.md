---
title: Implementierung und Reporting
description: In diesem Kapitel wird beschrieben, wie Sie die Player-Status-Tracking-Funktion implementieren, einschließlich .
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 58%

---


# Implementierung und Reporting

Während einer Wiedergabesitzung muss jedes Statusereignis (vom Beginn bis zum Ende) einzeln getrackt werden. Das Medien-SDK und die Mediensammlungs-API bieten neue Tracking-Methoden für diese Funktion.

Das Medien-SDK beinhaltet zwei neue Methoden zum Tracking benutzerdefinierter Status:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


The Media Collection API includes two new events that have `media.stateName` as the required parameter:

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

## Berichterstellung

Alle Player-Zustandsmetriken können für jede in Analysis Workspace verfügbare Visualisierung von Berichten oder für eine Komponente (Segment, berechnete Metriken) verwendet werden, sobald eine Report Suite für die Player-Zustandsverfolgung aktiviert ist. Die neuen Metriken können in der Admin-Konsole für jeden einzelnen Bericht über Media Berichte Setup (Einstellungen bearbeiten > Medienverwaltung > Media Berichte) aktiviert werden.

![](assets/report-setup.png)

In Analytics Workspace befinden sich alle neuen Eigenschaften im Metrikbedienfeld. Sie können z. B. `full screen` nach den Vollbilddaten im Metrikbedienfeld suchen.

![](assets/full-screen-report.png)

## Importieren der vom Player angegebenen Metriken in Adobe Experience Platform

In Analytics gespeicherte Daten können für jeden Zweck verwendet werden. Die Player-Statusmetriken können mithilfe von XDM in Adobe Experience Platform importiert und mit Customer Journey Analytics verwendet werden. Die Standardstatuseigenschaften haben bestimmte Eigenschaften, während die benutzerdefinierten Status Eigenschaften mit den benutzerdefinierten Ereignissen verfügbar sind. Weitere Informationen zu den Standardstatuseigenschaften finden Sie im Abschnitt *Eigenschaften-Liste für XDM-Identitäten* auf der Seite [Player-Statusparameter](/help/metrics-and-metadata/player-state-parameters.md) .
