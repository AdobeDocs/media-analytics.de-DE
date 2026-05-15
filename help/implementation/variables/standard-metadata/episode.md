---
title: Folge
description: Legen Sie die Episodennummer für episodischen Inhalt fest, damit einzelne Episoden separat gemeldet werden können.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 15%

---


# Folge

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Episode**&#x200B;behandelt. Siehe [Folge](/help/reporting/dimensions/episode.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Episodenvariable ist die Episodennummer innerhalb der Staffel (in der Regel eine ganze Zahl wie `"13"`). Kombinieren Sie mit [Show](/help/implementation/variables/standard-metadata/show.md) und [Staffel](/help/implementation/variables/standard-metadata/season.md), damit die Interaktion nach einzelnen Episoden unterbrochen werden kann.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.episode` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.episode` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`episode` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        episode: "13"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Folgenummer als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.EPISODE`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `episode` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "episode": "13"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `episode` in `mediaCollection.sessionDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "episode": "13"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Folge mithilfe von `ADB.Media.VideoMetadataKeys.Episode` an das `contextData`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "13";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.episode` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.episode": "13"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
