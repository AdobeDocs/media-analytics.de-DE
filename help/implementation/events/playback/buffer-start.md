---
title: Start der Pufferung
description: Signal, dass der Medienplayer einen Pufferzustand erreicht hat.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

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

>[!TAB Roku]

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

>[!TAB Media Collection API]

Senden Sie einen `bufferStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
