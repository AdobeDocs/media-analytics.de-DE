---
title: Gleichzeitiges Aktualisieren von mehreren Player-Status
description: In diesem Thema wird die Funktion „Statusverfolgung für mehrere Player“ beschrieben.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '186'
ht-degree: 100%

---

# Statusverfolgung für mehrere Player

Manchmal beginnen zwei Player-Status gleichzeitig und enden gleichzeitig oder das Ende eines Status ist auch der Anfang eines anderen Status, wie in der folgenden Abbildung zu sehen ist:

![Status von mehreren Playern](assets/multiple-player-states.png)

Die aktuelle Implementierung ermöglicht beide Szenarien:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Dazu müssen Sie jedoch mehrere `stateStart`- und `stateEnd`-Ereignisse ausgeben, um mehrere gleichzeitige Statusänderungen zu signalisieren. Um
dieses gängige Verhalten zu optimieren, wurde ein neuer `statesUpdate`-Ereignistyp implementiert, der eine Liste von Status beendet 
und eine Liste neuer Status startet.

Unter Verwendung des neuen `statesUpdate`-Ereignisses wird die obige Ereignisliste zu:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Die Anzahl der Statusaktualisierungsaufrufe wurde für dasselbe Verhalten von sechs auf drei reduziert. Das letzte Ereignis 
hätte auch ein einfaches `stateEnd(fullScreen)` sein können.

## Implementierung der Mediensammlungs-API {#mpst-api}

Sie können die Mediensammlungs-API verwenden, um die Statusverfolgung für mehrere Player zu implementieren.

### Beispiel

Im Folgenden finden Sie ein Beispiel für die Implementierung der Mediensammlungs-API für die Statusverfolgung mehrerer Player.

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

## Implementierung des Media SDK

Es gibt keine Media SDK-Implementierung.
