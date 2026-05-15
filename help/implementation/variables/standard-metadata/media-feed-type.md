---
title: Medien-Feed-Typ
description: Identifizieren Sie die Art des Broadcast-Feeds (z. B. East-HD oder West-SD) für Inhalte, die je nach Region oder Qualität variieren.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---


# Medien-Feed-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Medien-Feed-Typ**&#x200B;behandelt. Siehe [Medien-Feed-](/help/reporting/dimensions/media-feed-type.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable vom Typ Medien-Feed identifiziert den Broadcast-Feed (z. B. `"East-HD"`, `"West-SD"` oder `"4K"`). Verwenden Sie sie, wenn derselbe Inhalt über mehrere regionale oder hochwertige Feeds bereitgestellt wird und die Interaktion pro Feed aufgeschlüsselt werden muss.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.feed` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.feed` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`feed` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        feed: "East-HD"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Feed-Typ als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.MEDIA_FEED`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `feed` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "feed": "East-HD"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `feed` in `mediaCollection.sessionDetails` auf:

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
          "feed": "East-HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Feed im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.Feed`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Feed] = "East-HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.feed` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.feed": "East-HD"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
