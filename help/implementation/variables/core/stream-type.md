---
title: Stream-Typ
description: Legen Sie den Stream-Typ fest, um festzustellen, ob es sich bei einem Medien-Stream um Audio- oder Videoinhalte handelt.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---


# Stream-Typ

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Stream type**behandelt. Siehe [Stream-Typ](/help/reporting/dimensions/stream-type.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable vom Typ Stream gibt an, ob es sich bei einem Medien-Stream um Audio- oder Videoinhalte handelt. Sie ist für alle Implementierungen von Streaming-Medien erforderlich und muss zu Beginn jeder Mediensitzung festgelegt werden.

Das richtige Festlegen des Stream-Typs ist für die Berichterstellung für Streaming-Medien von grundlegender Bedeutung. Dadurch werden die integrierten **Media Stream Type**-Segmente in Adobe Analytics (All Media, Audio Only, Video Only) aktiviert und separate Audio- und Videoberichte in Customer Journey Analytics gesteuert. Außerdem wird sichergestellt, dass Sitzungsdaten in der gesamten Media Analytics-Pipeline korrekt klassifiziert werden. Sitzungen mit einem nicht festgelegten oder ungültigen Stream-Typ können in nachgelagerten Berichten gruppiert oder falsch klassifiziert werden.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.streamType` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Erforderlich** | Ja |
| **Gesendet mit** | Sitzungsbeginn, Sitzungsabschluss |

## Web SDK

`streamType` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

Übergeben Sie `Media.MediaType.Video` oder `Media.MediaType.Audio` als das `mediaType` Argument an `createMediaObject`. Beachten Sie, dass das `streamType` in `createMediaObject` die Variable für den Inhaltstyp (VOD, Live usw.) steuert, nicht diese Variable.

**iOS (SWIFT)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

`streamType` in `mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

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

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `streamType` in `mediaCollection.sessionDetails` auf:

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

## Medien-SDK

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

## Mediensammlungs-API

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

Die [ Anfragestruktur und alle erforderlichen Felder finden Sie ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) der Referenz zur Mediensammlungs-API-Sitzungen .
