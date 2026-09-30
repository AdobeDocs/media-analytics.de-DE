---
title: Kapitelposition
description: Legen Sie den Kapitelindex innerhalb des Inhalts fest. Die Kapitelposition ist erforderlich, damit die Kapitel-ID automatisch korrekt generiert wird.
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
source-wordcount: '255'
ht-degree: 6%
---

# Kapitelposition

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Kapitelposition**&#x200B;behandelt. Siehe [Kapitelposition](/help/reporting/dimensions/chapter-position.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Kapitelpositionsvariable ist der Index des Kapitels innerhalb des Inhalts, beginnend bei `1` (typisch) oder `0` (abhängig von Ihrer Konvention). Verwenden Sie einen stabilen Index pro Kapitel, damit dasselbe Kapitel sitzungsübergreifend aggregiert wird.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.chapter.position` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.chapterDetails.index`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.chapter.position` |
| **Erforderlich** | Nein (Mobile SDK); Ja (Edge, Mediensammlungs-API) |
| **Gesendet mit** | [Kapitelstart](/help/implementation/events/chapters/chapter-start.md), Kapitelschluss |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`index` in `xdm.mediaCollection.chapterDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

Übergeben Sie die Kapitelposition als zweites Argument an `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie die Kapitelposition als zweites Argument an `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

Legen Sie `index` in `xdm.mediaCollection.chapterDetails` fest, wenn Sie `sendMediaEvent` für `media.chapterStart` aufrufen:

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

Rufen Sie den [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart)-Endpunkt mit `index` in `xdm.mediaCollection.chapterDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Übergeben Sie die Kapitelposition als zweites Argument für `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",
  1,
  240,
  0
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

Übergeben Sie die Kapitelposition als zweites Argument für `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

Übergeben Sie die Kapitelposition als zweites Argument (`position`) an `adb_media_init_chapterinfo`:

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB Media Collection API]

Fügen Sie `media.chapter.index` in das `params` Ihrer `chapterStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.index": 1
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]
