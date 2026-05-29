---
title: Play
description: Signal, dass der Medien-Player in den Wiedergabestatus gewechselt ist.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 10%

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

>[!TAB Roku]

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

>[!TAB Media Collection API]

Senden Sie einen `play` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
