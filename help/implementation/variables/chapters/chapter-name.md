---
title: Name des Kapitels
description: Legen Sie den Anzeigenamen jedes Kapitels fest, damit das Reporting auf Kapitelebene nach Kapiteltitel unterteilt werden kann.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 13%

---


# Name des Kapitels

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Kapitelname**&#x200B;behandelt. Siehe [Kapitelname](/help/reporting/dimensions/chapter-name.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „Kapitelname“ ist der für Menschen lesbare Titel eines Kapitels (z. B. `"Pilot Episode - Opening"`). Legen Sie sie für jedes `media.chapterStart` fest, dessen Inhalt in Kapitel unterteilt ist.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.chapter.friendlyName` |
| **XDM-Sammlungsfeld** | [`mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.chapter.friendlyName` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Kapitelstart](/help/implementation/events/chapters/chapter-start.md), Kapitelschluss |

## Web SDK

`friendlyName` in `mediaCollection.chapterDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

Übergeben Sie den Kapitelnamen als erstes (`name`) Argument an `createChapterObject`.

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
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Legen Sie `friendlyName` in `mediaCollection.chapterDetails` fest, wenn Sie `sendMediaEvent` für `media.chapterStart` aufrufen:

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

Rufen Sie den [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)-Endpunkt mit `friendlyName` in `mediaCollection.chapterDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Kapitelnamen als erstes Argument für `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.chapter.friendlyName` in das `params` Ihrer `chapterStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
