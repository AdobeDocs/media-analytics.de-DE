---
title: Content-Typ
description: Legen Sie den Inhaltstyp fest, um das Format des Streams anzugeben (VOD, Live, Linear, Podcast, Song usw.).
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---


# Content-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Content-Typ**&#x200B;behandelt. Siehe [Inhaltstyp](/help/reporting/dimensions/content-type.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „Content-Typ“ identifiziert das Format des Streams (z. B. VOD, Live oder Linear für Video oder Podcast oder Hörbuch für Audio). Sie ist für alle Implementierungen von Streaming-Medien erforderlich und muss beim Sitzungsstart festgelegt werden. Von Adobe definierte Werte füllen die integrierten Inhaltstypsegmente und Berichte aus. Benutzerdefinierte Zeichenfolgen werden ebenfalls akzeptiert, stimmen jedoch nicht mit den integrierten Segmenten überein. Wenn nicht festgelegt, ist der Wert standardmäßig auf `missing_content_type` festgelegt.

Empfohlene Werte:

* **Video:** `vod`, `live`, `linear`, `ugc`, `dvod`
* **Audio:** `song`, `podcast`, `audiobook`, `radio`

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.contentType` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.contentType` |
| **Erforderlich** | Ja |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`contentType` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
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

Übergeben Sie die Konstante des Inhaltstyps als `streamType` Argument an `createMediaObject`. Verwenden Sie `MediaConstants.StreamType.*` Werte wie `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Hinweis: In der Mobile SDK steuert das `streamType`-Argument den Inhaltstyp. Die Variable Stream-Typ (Audio vs. Video) ist das separate `mediaType`.

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

`contentType` in `mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
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

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `contentType` in `mediaCollection.sessionDetails` auf:

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

Übergeben Sie eine `ADB.Media.StreamType.*` Konstante als viertes Argument an `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.contentType` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
