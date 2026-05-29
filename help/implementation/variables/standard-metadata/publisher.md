---
title: Publisher
description: Legen Sie den Herausgeber des Audioinhalts fest.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 10%

---


# Publisher

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Publisher**&#x200B;behandelt. Siehe [Publisher](/help/reporting/dimensions/publisher.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable publisher ist der Name des Herausgebers des Audioinhalts (z. B. ein Podcast-Netzwerk oder ein Hörbuchherausgeber). Verwenden Sie diese Option, um die Interaktion zwischen Herausgebern in einem kuratierten Audiokatalog zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.publisher` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.publisher` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`publisher` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

>[!TAB iOS]

Übergeben Sie den Herausgeber als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.AudioMetadataKeys.PUBLISHER`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie den Herausgeber als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.AudioMetadataKeys.PUBLISHER`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

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

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `publisher` in `xdm.mediaCollection.sessionDetails` auf:

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Übergeben Sie den Herausgeber im `contextData`-Objekt mithilfe von `ADB.Media.AudioMetadataKeys.Publisher`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Publisher] = "Northbridge Audio";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.AudioMetadataKeys.PUBLISHER` , um den Herausgeber in der `StandardMediaMetadata`-Eigenschaft des Medienobjekts festzulegen, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
