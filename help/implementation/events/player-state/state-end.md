---
title: Zustandsende
description: Signal, dass der Medien-Player den Status getrackter Player verlassen hat.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 13%

---


# Zustandsende

Das Status-End-Ereignis signalisiert, dass der Medien-Player einen verfolgten Status wie Vollbild, Stummschaltung oder Untertitel verlassen hat. Senden Sie ihn, um einen durch „State Start[&#x200B; geöffneten Status zu &#x200B;](state-start.md). Status können im selben Ereignisaufruf gestartet und beendet werden. Ein Player kann mehrere Status gleichzeitig verlassen.

Gültige Statusnamen: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Statusstart](state-start.md)
* **Zugeordnete Metrik**: Variiert je nach Status; siehe [Player-Statusverfolgung](/help/use-cases/player-state-tracking/implementation-and-reporting.md)

## Web SDK

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.statesUpdate"` und dem Statusnamen in `statesEnd` auf:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

Status können im selben Aufruf gestartet und beendet werden:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Verwenden Sie `trackPlayerStateEnd` mit einem Statusobjekt, das aus der entsprechenden `MediaConstants.PlayerState` erstellt wurde.

**iOS (SWIFT)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

## Roku (BrightScript)

Rufen Sie `sendMediaEvent` mit `eventType: "media.statesUpdate"` und dem Statusnamen in `statesEnd` auf:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

## Media Edge-API

Rufen Sie den [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)-Endpunkt mit dem Statusnamen in `statesEnd` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Verwenden Sie `ADB.Media.createStateObject` mit der entsprechenden `ADB.Media.PlayerState`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

## Mediensammlungs-API

Senden Sie einen `stateEnd` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
