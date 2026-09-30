---
title: Play
description: Signal, dass der Medien-Player in den Wiedergabestatus gewechselt ist.
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
source-wordcount: '187'
ht-degree: 9%
---

# Play

Das Wiedergabeereignis signalisiert, dass der Medienplayer den Status auf Wiedergabe geändert hat. Senden Sie sie beim ersten Start des Inhalts, bei der automatischen Wiedergabe und immer dann, wenn der Player nach einer Pause oder Pufferung fortgesetzt wird. Es gibt kein separates Wiederaufnahmeereignis. Ein Wiedergabeereignis nach [Start anhalten](pause-start.md) oder [Pufferstart](buffer-start.md) dient als Wiederaufnahme.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Inhaltsstarts]](/help/reporting/metrics/content-starts.md)

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.play"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Rufen Sie `trackPlay` auf, wenn der Medien-Player beginnt oder die Wiedergabe fortsetzt.

```swift
tracker.trackPlay()
```

>[!TAB Android]

Rufen Sie `trackPlay` auf, wenn der Medien-Player beginnt oder die Wiedergabe fortsetzt.

```kotlin
tracker.trackPlay()
```

>[!TAB Roku Edge]

`sendMediaEvent` mit `eventType: "media.play"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
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

Rufen Sie `trackPlay` auf, wenn der Medien-Player beginnt oder die Wiedergabe fortsetzt:

```javascript
tracker.trackPlay();
```

>[!TAB Chromecast]

Rufen Sie `trackPlay` auf, wenn der Medien-Player beginnt oder die Wiedergabe fortsetzt:

```javascript
ADBMobile.media.trackPlay();
```

>[!TAB Roku 2.x]

Rufen Sie `mediaTrackPlay` auf, wenn der Medien-Player beginnt oder die Wiedergabe fortsetzt:

```brightscript
ADBMobile().mediaTrackPlay()
```

>[!TAB Media Collection API]

Senden Sie einen `play` POST an den [events-Endpunkt](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
