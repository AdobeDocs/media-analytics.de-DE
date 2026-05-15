---
title: Publisher
description: Legen Sie den Herausgeber des Audioinhalts fest.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 16%

---


# Publisher

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Publisher**&#x200B;behandelt. Siehe [Publisher](/help/reporting/dimensions/publisher.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable publisher ist der Name des Herausgebers des Audioinhalts (z. B. ein Podcast-Netzwerk oder ein Hörbuchherausgeber). Verwenden Sie diese Option, um die Interaktion zwischen Herausgebern in einem kuratierten Audiokatalog zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.publisher` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.publisher`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.publisher` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`publisher` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        publisher: "Northbridge Audio"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Herausgeber als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.AudioMetadataKeys.PUBLISHER`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `publisher` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "publisher": "Northbridge Audio"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `publisher` in `mediaCollection.sessionDetails` auf:

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
          "publisher": "Northbridge Audio"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Herausgeber im `contextData`-Objekt mithilfe von `ADB.Media.AudioMetadataKeys.Publisher`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Publisher] = "Northbridge Audio";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.publisher` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.publisher": "Northbridge Audio"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
