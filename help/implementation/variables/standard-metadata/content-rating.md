---
title: Bewertung des Inhalts
description: Legen Sie die Inhaltsbewertung gemäß den Richtlinien für TV Parental oder Ihrem regionalen Bewertungssystem fest.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 14%

---


# Bewertung des Inhalts

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Inhaltsbewertung**&#x200B;behandelt. Siehe [Inhaltsbewertung](/help/reporting/dimensions/content-rating.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Inhaltsbewertungsvariable ist die Zielgruppenbewertung gemäß den TV Parental Guidelines (`"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`) oder einem beliebigen regionalen Bewertungssystem. Verwenden Sie diese Option, um die Interaktion und Anzeigenlast über verschiedene Bewertungsebenen hinweg zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.rating` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.rating` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`rating` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        rating: "TVPG"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Bewertung als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.RATING`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `rating` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "rating": "TVPG"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `rating` in `mediaCollection.sessionDetails` auf:

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
          "rating": "TVPG"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Bewertung im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.Rating`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Rating] = "TVPG";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.rating` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.rating": "TVPG"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
