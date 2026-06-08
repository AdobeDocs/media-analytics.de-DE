---
title: Player-Status verfolgen
description: Erfahren Sie mehr über Player-Status-Ereignisse und darüber, wie Sie Vollbild-, Stummschaltungs-, verdeckte Untertitel-, Bild-in-Bild- und Fokusstatus verfolgen können.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 12%

---


# Player-Status verfolgen

Player-Statusereignisse verfolgen, wie Viewer während einer Sitzung mit Player-Steuerelementen interagieren. Sie sind optional und für Core-Medien-Tracking-Implementierungen nicht erforderlich. Die fünf nachverfolgbaren Status sind: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` und `inFocus`.

Player-Statusereignisse sind nützlich, um die Nutzung von Barrierefreiheitsfunktionen zu verstehen, z. B. wie oft Viewer Untertitel aktivieren oder stumm schalten. Sie zeigen auch das Betrachtungsverhalten von Mustern wie Vollbildmodus im Vergleich zu Inline-Anzeige und Bild-in-Bild-Multitasking.

## Player-Ereignisse

| Player-Ereignis | Aktion |
| --- | --- |
| Player enter a state | Verbindungsstatus starten |
| Player verlässt einen Status | Verbindungsstatus beenden |

## Standardmäßige und benutzerdefinierte Status

Es stehen fünf standardmäßige Player-Status zur Verfügung und Sie können Ihre eigenen benutzerdefinierten Status hinzufügen.

| Standardstatusname | Medien-SDK-Konstante | Name der Mediensammlungs-API |
|----|----|----|
| Vollbild | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Untertitel | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Stummschaltung | `ADB.Media.PlayerState.Mute` | `mute` |
| Bild im Bild | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Im Fokus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Siehe [Player-Statusvariablen](/help/implementation/variables/player-state/) für die vollständige Variablenreferenz einschließlich XDM-Pfaden und Metrikdefinitionen.

**Benutzerdefinierte Status:** Sie können benutzerdefinierte Status erstellen, um zusätzliche Player-Verhaltensweisen zu erfassen, die für Ihre Anwendung spezifisch sind. Siehe die [Media API-Referenz: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/) für Details zum Erstellen benutzerdefinierter Statusobjekte.

## Implementierungsschritte

1. **Rufen Sie [Status Start](state-start.md)** auf, wenn der Player in einen der fünf verfolgbaren Status wechselt. Es können mehrere Status gleichzeitig aktiv sein und mehrere Status können im selben Ereignisaufruf gestartet werden.
1. **Rufen Sie [Status beenden](state-end.md)** auf, wenn der Player einen Status verlässt. Mehrere Status können im selben Ereignisaufruf beendet werden, und Status können in einem einzigen Aufruf gestartet und zusammen beendet werden.

## Richtlinien

* Eine Videositzung ist auf zehn Player-Status beschränkt.
* Jede Statuskombination ist zulässig.
* Wenn mehrere Player-Status übergeben werden, werden nur die ersten 10 beibehalten und nachgelagert an das Medien-Backend weitergeleitet.
* Die maximale Anzahl von 10 Zuständen gilt für alle Zustände, unabhängig davon, ob sie offen oder geschlossen sind.
* Ein Status kann mehrmals beginnen und enden und zählt als einzelner Status. Beispielsweise kann `closedCaptioning` fünfmal gestartet und gestoppt werden, zählt aber als ein Status.
* Der Player-Status wird für alle Wiedergabestatus berechnet (keine Aufteilung).
* Player-Status werden für jede einzelne Wiedergabesitzung erfasst. Der Player-Status wird nicht für alle Wiedergaben berechnet.
* Die Kenntnis des Anwendungsstatus wird nicht aufrechterhalten, nachdem ein Status beendet wurde. Nach dem Beenden eines Status muss der Status erneut gestartet werden, um das Tracking fortzusetzen.

## Gleichzeitiges Aktualisieren mehrerer Status

Auf XDM-basierten Plattformen können mehrere Statusänderungen mithilfe von Arrays in `statesStart` und `statesEnd` in einem einzelnen `statesUpdate`-Aufruf zusammengefasst werden. Bei Mobile SDKs ist für jede Statusänderung ein separater Aufruf erforderlich.

Die folgenden Beispiele beginnen gemeinsam mit Stummschaltung und Bild-in-Bild und wechseln dann zum Vollbildmodus.

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Mobile SDK unterstützt keine Batching-Verarbeitung - es wird für jede Statusänderung ein separater Aufruf gesendet.

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

Mobile SDK unterstützt keine Batching-Verarbeitung - es wird für jede Statusänderung ein separater Aufruf gesendet.

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku Edge]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Mehrere Statusänderungen erfordern separate Aufrufe.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

Mehrere Statusänderungen erfordern separate Aufrufe.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB Roku 2.x]

Player-Status-Tracking ist in der Roku 2.x-SDK nicht verfügbar. Verwenden Sie zum Nachverfolgen der Player-Status [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB Media Collection API]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## Lange Pause

Wenn eine Videositzung eine Pausendauer von mehr als 30 Minuten aufweist, erfordert die API eine neue Sitzung. Generieren Sie eine neue Sitzungs-ID und behalten Sie alle aktiven Status bei, damit sie direkt nach dem neuen `sessionStart`-Aufruf mit `stateStart` Ereignissen wiederhergestellt werden können.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Nachdem `sessionEnd` gesendet wurde, starten Sie eine neue Sitzung und senden Sie die aktiven Status sofort erneut:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## Zustandsmetriken

Für jeden verfolgten Status werden drei Metriken berechnet und beim Aufruf zum Schließen der Medien an Adobe Analytics gesendet:

| Metrik | Kontextdatenschlüssel | Beschreibung |
| --- | --- | --- |
| State Set | `a.media.states.[state.name].set = true` | `true`, ob der Status während der Wiedergabe mindestens einmal festgelegt wurde |
| Anzahl der Bundesstaaten | `a.media.states.[state.name].count = 4` | Häufigkeit, mit der der Status während der Wiedergabe aufgetreten ist |
| State Time | `a.media.states.[state.name].time = 240` | Gesamtzeit (Sekunden), die während der Wiedergabe im Status verbracht wurde |
