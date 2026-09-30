---
title: Start der Pufferung
description: Signal, dass der Medienplayer einen Pufferzustand erreicht hat.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 7%
---

# Start der Pufferung

Das Pufferstartereignis signalisiert, dass der Medien-Player in einen Pufferzustand übergegangen ist.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Pufferereignisse]](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**XDM-basierte APIs (Web SDK, Roku, Media Edge-API, Media Collection-API):** Es gibt keinen Buffer-Resume-Ereignistyp. Das Puffer-Ende wird abgeleitet, wenn Sie ein [`play`](play.md) nach dem `bufferStart` senden.
>
>**Mobile SDK:** Rufen Sie `trackEvent(BufferComplete)` auf, wenn der Player die Pufferung beendet, und rufen Sie dann `trackPlay()` auf, um die Wiedergabe fortzusetzen.

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Rufen Sie `trackEvent` mit `BufferStart` auf, wenn der Player in einen Pufferzustand wechselt, und `BufferComplete`, wenn er beendet wird.

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Rufen Sie `trackEvent` mit `BufferStart` auf, wenn der Player in einen Pufferzustand wechselt, und `BufferComplete`, wenn er beendet wird.

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Rufen Sie `trackEvent` mit dem `BufferStart` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

>[!TAB Chromecast]

Rufen Sie `trackEvent` mit `BufferStart` auf, wenn der Player in einen Pufferzustand wechselt, und `BufferComplete`, wenn er beendet wird:

```javascript
// Buffer starts
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);

// Buffer ends
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
```

>[!TAB Roku 2.x]

Rufen Sie `mediaTrackEvent` mit `MEDIA_BUFFER_START` auf, wenn der Player in einen Pufferzustand wechselt, und `MEDIA_BUFFER_COMPLETE`, wenn er beendet wird:

```brightscript
adb = ADBMobile()

' Buffer starts
adb.mediaTrackEvent(adb.MEDIA_BUFFER_START)

' Buffer ends
adb.mediaTrackEvent(adb.MEDIA_BUFFER_COMPLETE)
```

>[!TAB Media Collection API]

Senden Sie einen `bufferStart` POST an den [events-Endpunkt](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
