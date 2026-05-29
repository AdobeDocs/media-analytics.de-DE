---
title: Content-Typ
description: Legen Sie den Inhaltstyp fest, um das Format des Streams anzugeben (VOD, Live, Linear, Podcast, Song usw.).
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 5%

---


# Content-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Content-Typ**behandelt. Siehe [Inhaltstyp](/help/reporting/dimensions/content-type.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „Content-Typ“ identifiziert das Format des Streams (z. B. VOD, Live oder Linear für Video oder Podcast oder Hörbuch für Audio). Sie ist für alle Implementierungen von Streaming-Medien erforderlich und muss beim Sitzungsstart festgelegt werden. Von Adobe definierte Werte füllen die integrierten Inhaltstypsegmente und Berichte aus. Benutzerdefinierte Zeichenfolgen werden ebenfalls akzeptiert, stimmen jedoch nicht mit den integrierten Segmenten überein. Wenn nicht festgelegt, ist der Wert standardmäßig auf `missing_content_type` festgelegt.

Empfohlene Werte:

* **Video:** `vod`, `live`, `linear`, `ugc`, `dvod`
* **Audio:** `song`, `podcast`, `audiobook`, `radio`

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.contentType` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.contentType` |
| **Erforderlich** | Ja |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`contentType` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

>[!TAB iOS]

Übergeben Sie die Konstante des Inhaltstyps als `streamType` Argument an `createMediaObject`. Verwenden Sie `MediaConstants.StreamType.*` Werte wie `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Hinweis: In der Mobile SDK steuert das `streamType`-Argument den Inhaltstyp. Die Variable Stream-Typ (Audio vs. Video) ist das separate `mediaType`.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie die Konstante des Inhaltstyps als `streamType` Argument an `createMediaObject`. Verwenden Sie `MediaConstants.StreamType.*` Werte wie `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Hinweis: In der Mobile SDK steuert das `streamType`-Argument den Inhaltstyp. Die Variable Stream-Typ (Audio vs. Video) ist das separate `mediaType`.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

`contentType` in `xdm.mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

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

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `contentType` in `xdm.mediaCollection.sessionDetails` auf:

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Übergeben Sie eine `ADBMobile.media.StreamType.*` Konstante als viertes Argument an `ADBMobile.media.createMediaObject`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

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

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
