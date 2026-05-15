---
title: Inhaltswiederaufnahmen
description: Markieren Sie eine Sitzung, bei der eine zuvor unterbrochene Wiedergabe fortgesetzt wird, damit das Backend ein Ereignis zur Wiederaufnahme von Inhalten zählt.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 11%

---


# Inhaltswiederaufnahmen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Inhaltswiederaufnahmen**behandelt. Siehe [Inhaltswiederaufnahmen](/help/reporting/metrics/content-resumes.md) für die entsprechende Berichtsmetrik.*

>[!ENDSHADEBOX]

Die Variable „Inhalt wird fortgesetzt“ kennzeichnet eine Sitzung, durch die eine zuvor unterbrochene Wiedergabe fortgesetzt wird. Legen Sie sie auf `media.sessionStart` fest, damit das Backend ein Content Resume-Ereignis für die Sitzung zählt und es aus den Zählungen für neue Streams ausschließt. Bei direkten API- und Edge-API-Implementierungen ist der Client dafür verantwortlich, wiederaufgenommene Sitzungen zu erkennen (z. B. nach einem Puffer, einer Pause oder einem Anhalten von mehr als 30 Minuten) und dieses Flag entsprechend festzulegen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.resume` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | nicht angegeben |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md) |

## Web SDK

Setzen Sie `hasResume` auf `true` in `mediaCollection.sessionDetails`, wenn Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) für die wiederaufgenommene Sitzung aufrufen:

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
        streamType: "video",
        hasResume: true
      },
      playhead: 60
    }
  }
});
```

## Mobile SDK

Übergeben Sie das Wiederaufnahme-Flag als Teil des optionalen Konfigurations-Bundles des Medienobjekts auf `trackSessionStart`. Verwenden Sie die `MediaConstants.MediaObjectKey.RESUMED`.

**iOS (SWIFT)**

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Setzen Sie `hasResume` auf `true` in `mediaCollection.sessionDetails`, wenn Sie `createMediaSession` für die wiederaufgenommene Sitzung aufrufen:

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
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 60
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt auf, wobei `hasResume` auf `true` in `mediaCollection.sessionDetails` festgelegt ist:

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

## Medien-SDK

Legen Sie den `RESUMED` Schlüssel für das Medieninformationsobjekt fest, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.resume` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
