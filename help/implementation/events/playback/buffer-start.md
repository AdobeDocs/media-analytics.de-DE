---
title: Start der Pufferung
description: Signal, dass der Medienplayer einen Pufferzustand erreicht hat.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 15%

---


# Start der Pufferung

Das Pufferstartereignis signalisiert, dass der Medien-Player in einen Pufferzustand übergegangen ist.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [Pufferereignisse](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**XDM-basierte APIs (Web SDK, Roku, Media Edge-API, Media Collection-API):** Es gibt keinen Buffer-Resume-Ereignistyp. Das Puffer-Ende wird abgeleitet, wenn Sie ein [`play`](play.md) nach dem `bufferStart` senden.
>
>**Mobile SDK:** Rufen Sie `trackEvent(BufferComplete)` auf, wenn der Player die Pufferung beendet, und rufen Sie dann `trackPlay()` auf, um die Wiedergabe fortzusetzen.

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.bufferStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackEvent` mit `BufferStart` auf, wenn der Player in einen Pufferzustand wechselt, und `BufferComplete`, wenn er beendet wird.

**iOS (SWIFT)**

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.bufferStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge-API

Rufen Sie den [bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackEvent` mit dem `BufferStart` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

## Mediensammlungs-API

Senden Sie einen `bufferStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```
