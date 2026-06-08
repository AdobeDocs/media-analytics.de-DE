---
title: Zustandsende
description: Signal, dass der Medien-Player den Status getrackter Player verlassen hat.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# Zustandsende

Das Status-End-Ereignis signalisiert, dass der Medien-Player einen verfolgten Status wie Vollbild, Stummschaltung oder Untertitel verlassen hat. Senden Sie ihn, um einen durch „State Start[&#x200B; geöffneten Status zu &#x200B;](state-start.md). Status können im selben Ereignisaufruf gestartet und beendet werden. Ein Player kann mehrere Status gleichzeitig verlassen.

Gültige Statusnamen: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Statusstart](state-start.md)
* **Zugehörige Metrik**: Variiert je nach Status; siehe [Player-Status verfolgen](/help/implementation/events/player-state/overview.md)

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Verwenden Sie `trackPlayerStateEnd` mit einem Statusobjekt, das aus der entsprechenden `MediaConstants.PlayerState` erstellt wurde.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

>[!TAB Android]

Verwenden Sie `trackPlayerStateEnd` mit einem Statusobjekt, das aus der entsprechenden `MediaConstants.PlayerState` erstellt wurde.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Verwenden Sie `ADB.Media.createStateObject` mit der entsprechenden `ADB.Media.PlayerState`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.createStateObject` mit der entsprechenden `ADBMobile.media.PlayerState`:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Player-Status-Tracking ist in der Roku 2.x-SDK nicht verfügbar. Verwenden Sie zum Nachverfolgen der Player-Status [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB Media Collection API]

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

>[!ENDTABS]
