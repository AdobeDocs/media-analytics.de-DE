---
title: Inhaltsname
description: Legen Sie den Anzeigenamen des Inhalts fest (der in Berichten angezeigte, für Menschen lesbare Titel).
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 15%

---


# Inhaltsname

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Content-Name**behandelt. Siehe [Inhaltsname](/help/reporting/dimensions/content-name.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Inhaltsnamenvariable ist der für Menschen lesbare Titel des Inhalts (z. B. `"Blinding Light"`). Dies ist optional, wird aber dringend empfohlen. Im XDM-Schema wird es `friendlyName` zugeordnet (nicht `name`; `name` enthält die Inhalts-ID).

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.friendlyName` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.friendlyName` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`friendlyName` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "Blinding Light",
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

Übergeben Sie den für Menschen lesbaren Namen als erstes (`name`) Argument an `createMediaObject`. Das zweite Argument ist die Inhalts-ID.

**iOS (SWIFT)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "Blinding Light",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("Blinding Light",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

`friendlyName` in `mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "Blinding Light",
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

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `friendlyName` in `mediaCollection.sessionDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "friendlyName": "Blinding Light",
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

Übergeben Sie den für Menschen lesbaren Namen als erstes Argument an `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "Blinding Light",    // name (friendly name)
  "video-123",              // media ID
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.name` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.name": "Blinding Light"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
