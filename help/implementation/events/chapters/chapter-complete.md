---
title: Kapitel abgeschlossen
description: Signal, dass die Wiedergabe eines Kapitelsegments abgeschlossen ist.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 20%

---


# Kapitel abgeschlossen

Das Ereignis „Chapter Complete“ signalisiert, dass die Wiedergabe eines Kapitels abgeschlossen ist. Senden, wenn der Viewer das Ende eines Kapitels erreicht. Wenn der Viewer das Kapitel überspringt, senden Sie stattdessen [Kapitelüberspringen](chapter-skip.md).

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Kapitelstart](chapter-start.md)
* **Zugeordnete Metrik**: [Kapitel abgeschlossen](/help/reporting/metrics/chapter-completes.md)

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.chapterComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackEvent` mit dem `ChapterComplete` Ereignistyp auf.

**iOS (SWIFT)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.chapterComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

## Media Edge-API

Rufen Sie den [chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackEvent` mit dem `ChapterComplete` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

## Mediensammlungs-API

Senden Sie einen `chapterComplete` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```
