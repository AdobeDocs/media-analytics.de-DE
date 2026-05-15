---
title: Netzwerk
description: Broadcast-Netzwerk oder Kanalnamen einstellen.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 16%

---


# Netzwerk

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Network**&#x200B;behandelt. Siehe [Netzwerk](/help/reporting/dimensions/network.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Netzwerkvariable ist der Broadcast-Netzwerk- oder Kanalname (z. B. `"Fox"`, `"ESPN"` oder `"HBO"`). Verwenden Sie diese Option, um die Interaktion zwischen Netzwerken innerhalb derselben Streaming-Eigenschaft zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.network` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.network`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.network` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`network` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        network: "ESPN"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Netzwerknamen als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.NETWORK`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.NETWORK] = "ESPN"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.NETWORK] = "ESPN"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `network` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "network": "ESPN"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `network` in `mediaCollection.sessionDetails` auf:

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
          "network": "ESPN"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie das Netzwerk im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.Network`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Network] = "ESPN";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.network` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.network": "ESPN"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
