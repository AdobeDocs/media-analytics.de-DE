---
title: Mehrere Player-Status gleichzeitig aktualisieren
description: In diesem Thema wird die Funktion "Mehrfach-Player-Status-Tracking"beschrieben.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7a28674024739593431a942d5e0a498294bbe793
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 10%

---

# Verfolgung mehrerer Player-Status

Es gibt Situationen, in denen zwei Player-Status gleichzeitig beginnen und enden oder wenn das Ende eines Status auch der Anfang eines anderen Status ist. Sehen Sie sich folgendes Beispiel an:

![Mehrere Player-Status](assets/multiple-player-states.svg)

Die aktuelle Implementierung ermöglicht beide Szenarien:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Der Client muss jedoch viele `stateStart` und `stateEnd` -Ereignisse, um mehrere gleichzeitige Statusänderungen zu signalisieren. Um dieses gemeinsame Verhalten zu optimieren, wird ein neuer `statesUpdate` -Ereignistyp implementiert wurde, der eine Liste von Status beendet und eine Liste neuer Status startet.

Neue `statesUpdate` -Ereignis, wird die obige Ereignisliste zu:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Die Anzahl der Aufrufe zur Statusaktualisierung wurde für dasselbe Verhalten von 6 auf nur 3 reduziert. Das letzte Ereignis hätte auch eine einfache `stateEnd(fullScreen)`.

## Implementierung der Mediensammlungs-API

Beispiele:

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Implementierung des Medien-SDK

Es gibt keine Media SDK-Implementierung.
