---
title: Kapitelstart
description: Signalisieren Sie den Beginn eines Kapitelsegments im Inhalt.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 17%

---


# Kapitelstart

Das Ereignis „Kapitelstart“ signalisiert den Beginn eines Kapitels im Inhalt. Das Kapitel-Tracking ist optional und für das Core-Medien-Tracking nicht erforderlich.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [Kapitelstarts](/help/reporting/metrics/chapter-starts.md)

## Web SDK

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.chapterStart"` und den erforderlichen `chapterDetails` auf:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Kapitelnamen, die Position, die Länge und die Startzeit an `createChapterObject` und rufen Sie dann `trackEvent` auf.

**iOS (SWIFT)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1,
                                              240,
                                              0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Rufen Sie `sendMediaEvent` mit `eventType: "media.chapterStart"` und den erforderlichen `chapterDetails` auf:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)-Endpunkt mit den erforderlichen `chapterDetails` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "chapterDetails": {
          "index": 1,
          "length": 240,
          "offset": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Übergeben Sie den Kapitelnamen, die Position, die Länge und die Startzeit an `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, null);
```

## Mediensammlungs-API

Senden Sie einen `chapterStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening",
    "media.chapter.index": 1,
    "media.chapter.offset": 0,
    "media.chapter.length": 240
  }
}
```
