---
title: Kapitelstart
description: Signalisieren Sie den Beginn eines Kapitelsegments im Inhalt.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# Kapitelstart

Das Ereignis „Kapitelstart“ signalisiert den Beginn eines Kapitels im Inhalt. Das Kapitel-Tracking ist optional und für das Core-Medien-Tracking nicht erforderlich. Kapitel dürfen sich nicht überschneiden. Senden Sie [Kapitel abgeschlossen](chapter-complete.md) oder [Kapitelüberspringen](chapter-skip.md), um das aktuelle Kapitel zu schließen, bevor Sie ein neues beginnen.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Kapitelstarts]](/help/reporting/metrics/chapter-starts.md)

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Übergeben Sie den Kapitelnamen, die Position, die Länge und die Startzeit an `createChapterObject` und rufen Sie dann `trackEvent` auf.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie den Kapitelnamen, die Position, die Länge und die Startzeit an `createChapterObject` und rufen Sie dann `trackEvent` auf.

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1,
                                              240,
                                              0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Übergeben Sie den Kapitelnamen, die Position, die Länge und die Startzeit an `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

Erstellen Sie ein Kapitelobjekt mit `adb_media_init_chapterinfo` und verfolgen Sie dann das Ereignis:

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
