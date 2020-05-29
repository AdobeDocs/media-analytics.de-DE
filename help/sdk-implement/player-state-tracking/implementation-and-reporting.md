---
title: Implementierung und Berichte
description: In diesem Thema wird beschrieben, wie Sie die Player-Statusverfolgungsfunktion implementieren, einschließlich .
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Implementierung und Berichte

Während einer Wiedergabesitzung muss jedes Zustandsereignis (von Beginn zu Ende) einzeln verfolgt werden. Das Media SDK und die Media Collection API bieten neue Verfolgungsmethoden für diese Funktion.

Das Media SDK umfasst zwei neue Methoden zur Verfolgung benutzerdefinierter Zustände:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Die Media Collection-API enthält zwei neue Ereignis, die `media.stateName` als erforderlichen Parameter verwendet werden:

`stateStart` und `stateEnd`

## Media SDK-Implementierung

Player State-Beginn

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Player-Status beendet

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## API-Implementierung für die Medienerfassung

Player State-Beginn

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

Player-Status beendet

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

Die für die einzelnen Statusangaben bereitgestellten Metriken werden berechnet, als Kontextdatenparameter an Adobe Analytics gesendet und zu Berichte gespeichert. Für jeden Status stehen drei Metriken zur Verfügung:

* `a.media.states.[state.name].set = true` — Auf &quot;true&quot;setzen, wenn der Status für jede einzelne Wiedergabe eines Streams mindestens einmal festgelegt wurde.
* `a.media.states.[state.name].count = 4` — Identifiziert die Anzahl der Vorkommen eines Status während jeder einzelnen Wiedergabe eines Streams
* `a.media.states.[state.name].time = 240` — Identifiziert die Gesamtstatusdauer in Sekunden pro einzelner Wiedergabe eines Streams

## Berichterstellung

Alle Player-Statusmetriken können für jede in Analyse Workspace oder einer  verfügbare Visualisierung von Berichten (Segment, berechnete Metriken) verwendet werden, sobald eine Report Suite für die Player-Statusverfolgung aktiviert ist. Die neuen Metriken können in der Admin-Konsole für jeden einzelnen Bericht über Media Berichte Setup (Einstellungen bearbeiten > Medienverwaltung > Media Berichte) aktiviert werden.

![](assets/report-setup.png)

In Analytics Workspace befinden sich alle neuen Eigenschaften im Metrikbedienfeld. Sie können z. B. `full screen` nach den Vollbilddaten im Metrikbedienfeld suchen.

![](assets/full-screen-report.png)

## Importieren von vom Player angegebenen Metriken in Adobe Experience Platform

In Analytics gespeicherte Daten können für jeden Zweck verwendet werden. Die Player-Statusmetriken können mithilfe von XDM in Adobe Experience Platform importiert und mit Customer Journey Analytics verwendet werden. Die Standardstatuseigenschaften haben bestimmte Eigenschaften, während die benutzerdefinierten Status Eigenschaften über die benutzerdefinierten Ereignis verfügbar sind.
