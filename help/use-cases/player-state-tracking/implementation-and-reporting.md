---
title: Implementierung und Reporting
description: Erfahren Sie, wie Sie die Player-Status-Tracking-Funktion implementieren einschließlich
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 15cc123fb44654083b6501042bdd9d4e07128b59
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 78%

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

## Berichterstellung

Alle Player-Statusmetriken können für jede in Analysis Workspace verfügbare Visualisierung von Berichten oder für eine Komponente (Segment, berechnete Metriken) verwendet werden, sobald eine Report Suite für das Player-Status-Tracking aktiviert wurde. Diese Metriken können in der Admin Console für jeden einzelnen Bericht mithilfe der Einrichtung der Medienberichte (Einstellungen bearbeiten > Medienverwaltung > Medienberichte) aktiviert werden.

![](assets/report-setup.png)

In Analysis Workspace befinden sich alle neuen Eigenschaften im Bedienfeld Metriken . Sie können beispielsweise nach `full screen` suchen, um die Vollbilddaten im Metrikbedienfeld anzuzeigen.

![](assets/full-screen-report.png)

## Importieren der vom Player angegebenen Metriken in Adobe Experience Platform

In Analytics gespeicherte Daten können für jeden Zweck verwendet werden. Die Player-Statusmetriken können mithilfe von XDM in Adobe Experience Platform importiert und mit Customer Journey Analytics verwendet werden. Die Standardstatuseigenschaften haben bestimmte Eigenschaften, während die benutzerdefinierten Statuseigenschaften über die benutzerdefinierten Ereignisse verfügbar sind. Zusätzliche Informationen zu den Standardstatuseigenschaften finden Sie im Abschnitt mit der *Eigenschaftenliste für XDM-Identitäten* auf der Seite [Player-Statusparameter](/help/implementation/variables/player-state-parameters.md).
