---
title: Versatz des Kapitels
description: Legen Sie den Versatz des Kapitels innerhalb des Inhalts in Sekunden ab Beginn fest.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 12%

---


# Versatz des Kapitels

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Chapter Offset**behandelt. Siehe [Kapitelversatz](/help/reporting/dimensions/chapter-offset.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable für den Kapitelversatz ist der Versatz des Kapitels innerhalb des Inhalts, gemessen in Sekunden ab Beginn. Das erste Kapitel hat in der Regel `0`. Nachfolgende Kapitel haben Versätze, die mit ihrer Abspielkopfstartzeit übereinstimmen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.chapter.offset` |
| **XDM-Sammlungsfeld** | [`mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.chapter.offset` |
| **Erforderlich** | Nein (Mobile SDK); Ja (Edge, Mediensammlungs-API) |
| **Gesendet mit** | [Kapitelstart](/help/implementation/events/chapters/chapter-start.md), Kapitelschluss |

## Web SDK

`offset` in `mediaCollection.chapterDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Versatz in Sekunden als viertes Argument (`startTime`) an `createChapterObject`.

**iOS (SWIFT)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Legen Sie `offset` in `mediaCollection.chapterDetails` fest, wenn Sie `sendMediaEvent` für `media.chapterStart` aufrufen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

## Media Edge-API

Rufen Sie den [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)-Endpunkt mit `offset` in `mediaCollection.chapterDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Versatz als viertes Argument an `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.chapter.offset` in das `params` Ihrer `chapterStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

Die vollständige Anfragestruktur [ Sie in der ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
