---
title: Stream-Typ
description: Legen Sie den Stream-Typ fest, um festzustellen, ob es sich bei einem Medien-Stream um Audio- oder Videoinhalte handelt.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 6%

---


# Stream-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Stream type**&#x200B;behandelt. Siehe [Stream-Typ](/help/reporting/dimensions/stream-type.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable vom Typ Stream gibt an, ob es sich bei einem Medien-Stream um Audio- oder Videoinhalte handelt. Sie ist für alle Implementierungen von Streaming-Medien erforderlich und muss zu Beginn jeder Mediensitzung festgelegt werden.

Das richtige Festlegen des Stream-Typs ist für die Berichterstellung für Streaming-Medien von grundlegender Bedeutung. Dadurch werden die integrierten **Media Stream Type**-Segmente in Adobe Analytics (All Media, Audio Only, Video Only) aktiviert und separate Audio- und Videoberichte in Customer Journey Analytics gesteuert. Außerdem wird sichergestellt, dass Sitzungsdaten in der gesamten Media Analytics-Pipeline korrekt klassifiziert werden. Sitzungen mit einem nicht festgelegten oder ungültigen Stream-Typ können in nachgelagerten Berichten gruppiert oder falsch klassifiziert werden.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.streamType` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.streamType` |
| **Erforderlich** | Ja |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`streamType` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

>[!TAB iOS]

Übergeben Sie `Media.MediaType.Video` oder `Media.MediaType.Audio` als das `mediaType` Argument an `createMediaObject`. Beachten Sie, dass das `streamType` in `createMediaObject` die Variable für den Inhaltstyp (VOD, Live usw.) steuert, nicht diese Variable.

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie `Media.MediaType.Video` oder `Media.MediaType.Audio` als das `mediaType` Argument an `createMediaObject`. Beachten Sie, dass das `streamType` in `createMediaObject` die Variable für den Inhaltstyp (VOD, Live usw.) steuert, nicht diese Variable.

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

`streamType` in `xdm.mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

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

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `streamType` in `xdm.mediaCollection.sessionDetails` auf:

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
          "streamType": "video"
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

Übergeben Sie `ADB.Media.MediaType.Video` oder `ADB.Media.MediaType.Audio` als fünftes Argument an `Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Übergeben Sie `ADBMobile.media.MediaType.Video` oder `ADBMobile.media.MediaType.Audio` als fünftes Argument an `ADBMobile.media.createMediaObject`:

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

>[!TAB Roku 2.x]

Übergeben Sie `MEDIA_TYPE_VIDEO` oder `MEDIA_TYPE_AUDIO` als fünftes (`mediaType`) Argument an `adb_media_init_mediainfo`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

Fügen Sie `media.streamType` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

Die [&#x200B; Anfragestruktur und alle erforderlichen Felder finden Sie &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) der Referenz zur Mediensammlungs-API-Sitzungen .

>[!ENDTABS]
