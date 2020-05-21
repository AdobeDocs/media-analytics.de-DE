---
title: Implementierung und Berichte
description: In diesem Thema wird beschrieben, wie Sie die Player-Statusverfolgungsfunktion implementieren, einschließlich .
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Implementierung und Berichte

Während einer Wiedergabesitzung muss jedes Zustandsereignis (von Beginn zu Ende) einzeln verfolgt werden. Das Media SDK und die Media Collection API bieten neue Verfolgungsmethoden für diese Funktion.

Das Media SDK umfasst zwei neue Methoden zur Verfolgung benutzerdefinierter Zustände:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Die Media Collection-API enthält zwei neue Ereignis mit dem erforderlichen Parameter &quot;media.stateName&quot;:

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

* `a.media.states.(media.state.name).set = true` — Auf &quot;true&quot;setzen, wenn der Status für jede einzelne Wiedergabe eines Streams mindestens einmal festgelegt wurde.
* `a.media.states.(media.state.name).count = 4` — Identifiziert die Anzahl der Vorkommen eines Status während jeder einzelnen Wiedergabe eines Streams
* `a.media.states.(media.state.name).time = 240` — Identifiziert die Gesamtstatusdauer in Sekunden pro einzelner Wiedergabe eines Streams

## Berichterstellung

Alle Statusmetriken können für jede beliebige Visualisierung oder Komponente (Berichte, berechnete Metriken) verwendet werden.
TBD - Quelle/Wiki für aktuelle Informationen überprüfen - für Screenshot von AW

## Importieren von vom Player angegebenen Metriken in Adobe Experience Platform

In Analytics gespeicherte Daten können für jeden Zweck verwendet werden. Die Player-Statusmetriken können mithilfe von XDM in Adobe Experience Platform importiert und mit Customer Journey Analytics verwendet werden. Die Standardstatuseigenschaften haben bestimmte Eigenschaften, während die benutzerdefinierten Status Eigenschaften über die benutzerdefinierten Ereignis verfügbar sind. Weitere Informationen finden Sie in der Liste Eigenschaften für XDM-Identitäten unter ?LINK TO METRIC-LISTE?.
