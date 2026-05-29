---
title: Zustandsstart
description: Signal, dass der Medienplayer in den Status „Getrackter Player“ übergegangen ist.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---


# Zustandsstart

Das Status-Startereignis signalisiert, dass der Medien-Player in einen verfolgten Status wie Vollbild, Stummschaltung oder Untertitel übergegangen ist. Ein Player kann sich gleichzeitig in mehreren Status befinden und Status können im selben Ereignisaufruf gestartet und beendet werden. Schließen Sie jeden Status mit einem [State End](state-end.md)-Ereignis.

Gültige Statusnamen: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugehörige Metrik**: Variiert je nach Status; siehe [Player-Status verfolgen](/help/implementation/events/player-state/overview.md)

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.statesUpdate"` und dem Statusnamen in `statesStart` auf:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Im selben Aufruf können mehrere Status gestartet werden:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

Verwenden Sie `trackPlayerStateStart` mit einem Statusobjekt, das aus der entsprechenden `MediaConstants.PlayerState` erstellt wurde.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

>[!TAB Android]

Verwenden Sie `trackPlayerStateStart` mit einem Statusobjekt, das aus der entsprechenden `MediaConstants.PlayerState` erstellt wurde.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

>[!TAB Roku]

Rufen Sie `sendMediaEvent` mit `eventType: "media.statesUpdate"` und dem Statusnamen in `statesStart` auf:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)-Endpunkt mit dem Statusnamen in `statesStart` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
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

tracker.trackPlayerStateStart(stateObject);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.createStateObject` mit der entsprechenden `ADBMobile.media.PlayerState`:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
```

>[!TAB Media Collection API]

Senden Sie einen `stateStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
