---
title: Stream-Format
description: Legen Sie das Stream-Format fest, um die Qualitätsstufe (HD, SD oder eine andere Bezeichnung, die Ihre Bereitstellungs-Pipeline verwendet) festzulegen.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# Stream-Format

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Stream-Format**&#x200B;behandelt. Siehe [Stream-Format](/help/reporting/dimensions/stream-format.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „stream format“ identifiziert die Qualitätsstufe des Streams (normalerweise `"HD"` oder `"SD"`, aber jede Zeichenfolge wird akzeptiert). Legen Sie ihn fest, wenn Sie Interaktionen, den Abschluss oder die Qualität nach Versandqualitätsstufe unterbrechen möchten.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.format` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.format` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`streamFormat` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        streamFormat: "HD"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie das Stream-Format als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.STREAM_FORMAT`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `streamFormat` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "streamFormat": "HD"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `streamFormat` in `mediaCollection.sessionDetails` auf:

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
          "streamFormat": "HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie das Stream-Format mithilfe von `ADB.Media.VideoMetadataKeys.StreamFormat` in das `contextData`-Objekt:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.StreamFormat] = "HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.streamFormat` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamFormat": "HD"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
