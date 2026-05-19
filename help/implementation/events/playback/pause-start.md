---
title: Start anhalten
description: Signal, dass die Medienwiedergabe angehalten wurde.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 19%

---


# Start anhalten

Das Pause-Start-Ereignis signalisiert, dass der Benutzer die Wiedergabe angehalten hat. Es gibt kein separates Fortsetzungsereignis. Senden Sie ein [Play](play.md)-Ereignis, wenn die Wiedergabe fortgesetzt wird.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [Ereignisse anhalten](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>Es gibt keinen Resume-Ereignistyp. Eine Wiederaufnahme wird abgeleitet, wenn Sie nach der `pauseStart` ein [`play`](play.md) Ereignis senden.

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.pauseStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

## Mobile SDK

Ruft `trackPause` auf, wenn der Benutzer die Wiedergabe pausiert.

**iOS (SWIFT)**

```swift
tracker.trackPause()
```

**Android (Kotlin)**

```kotlin
tracker.trackPause()
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.pauseStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

## Media Edge-API

Rufen Sie den [pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

`trackPause` aufrufen, wenn der Benutzer die Wiedergabe pausiert:

```javascript
tracker.trackPause();
```

## Mediensammlungs-API

Senden Sie einen `pauseStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```
