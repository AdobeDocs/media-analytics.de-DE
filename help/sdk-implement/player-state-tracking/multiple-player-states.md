---
title: Mehrere Player-Status gleichzeitig aktualisieren
description: In diesem Thema wird die Funktion "Mehrfach-Player-Status-Tracking"beschrieben.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fdbb777547181422b81ff6f7874bec3d317d02e9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 9%

---

# Verfolgung mehrerer Player-Status

Manchmal beginnen und enden zwei Player-Status gleichzeitig oder das Ende eines Status ist auch der Anfang eines anderen Status, wie in der folgenden Abbildung dargestellt:

![Mehrere Player-Status](assets/multiple-player-states.svg)

Die aktuelle Implementierung ermöglicht beide Szenarien:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Dazu müssen Sie jedoch mehrere `stateStart` und `stateEnd` -Ereignisse, um mehrere gleichzeitige Statusänderungen zu signalisieren. Um dieses gemeinsame Verhalten zu optimieren, wird ein neuer `statesUpdate` -Ereignistyp implementiert wurde, der eine Liste von Status beendet und eine Liste neuer Status startet.

Neue `statesUpdate` -Ereignis, wird die obige Ereignisliste zu:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Die Anzahl der Aufrufe zur Statusaktualisierung wurde für dasselbe Verhalten von sechs auf drei reduziert. Das letzte Ereignis hätte auch eine einfache `stateEnd(fullScreen)`.

## Implementierung der Mediensammlungs-API {#mpst-api}

Sie können die Mediensammlungs-API verwenden, um das Tracking mehrerer Player-Status zu implementieren.

### Beispiel

Im Folgenden finden Sie ein Beispiel für die Implementierung der Mediensammlungs-API für das Tracking mehrerer Player-Status.

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
