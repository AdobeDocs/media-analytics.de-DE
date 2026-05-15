---
title: Inhalts-ID
description: Medieninhalte eindeutig identifizieren.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 15%

---


# Inhalts-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Content ID**&#x200B;behandelt. Siehe [Inhalt](/help/reporting/dimensions/content.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „content id“ identifiziert jedes Medieninhalt eindeutig. Sie ist für alle Implementierungen von Streaming-Medien erforderlich und ist der Primärschlüssel für die Dimension „Inhaltsberichterstellung“. Setzen Sie ihn beim Sitzungsstart, und halten Sie ihn über alle Sitzungen hinweg für dasselbe Asset stabil.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.name` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.name` |
| **Erforderlich** | Ja |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`name` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Inhalts-ID als `mediaId` an `createMediaObject`.

**iOS (SWIFT)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

`name` in `mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `name` (der Inhalts-ID) in `mediaCollection.sessionDetails` auf:

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
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Inhalts-ID als zweites Argument für `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name (friendly name)
  "video-123",              // media ID — Content ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.id` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.id": "video-123"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
