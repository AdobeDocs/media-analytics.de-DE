---
title: Sitzungsstart
description: Signalisieren Sie den Beginn einer Mediensitzung und erhalten Sie die Sitzungs-ID, die für alle nachfolgenden Ereignisse erforderlich ist.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 12%

---


# Sitzungsstart

Das Sitzungsstartereignis öffnet eine Medienverfolgungssitzung. Es muss das erste Ereignis sein, das für eine Wiedergabe gesendet wird. Die Antwort gibt eine Sitzungs-ID zurück, die alle nachfolgenden Ereignisse für dieselbe Sitzung enthalten müssen.

* **Voraussetzungen**: Keine; immer das erste Ereignis
* **Zugeordnete Metrik**: [Medienstarts](/help/reporting/metrics/media-starts.md)

## Web SDK

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.sessionStart"` und den erforderlichen `sessionDetails` auf. Die Antwort enthält die Sitzungs-ID in `handle[].payload[].sessionId` (Typ `media-analytics:new-session`). Speichern Sie diesen Wert und übergeben Sie ihn als `sessionID` in allen nachfolgenden Ereignissen.

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

Rufen Sie `trackSessionStart` mit einem Medienobjekt und optionalen Metadaten auf.

**iOS (SWIFT)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku (BrightScript)

Rufen Sie `createMediaSession` mit den erforderlichen Sitzungsdetails an:

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

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt auf. Die Antwort enthält die Sitzungs-ID in `handle[].payload[].sessionId` (Typ `media-analytics:new-session`).

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackSessionStart` mit einem Medienobjekt auf, das mit `ADB.Media.createMediaObject` erstellt wurde:

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## Mediensammlungs-API

Senden Sie einen `sessionStart` POST an den [sessions-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md). Die Kopfzeile der `Location` enthält die Sitzungs-ID, die in allen nachfolgenden Ereignisanfragen verwendet werden soll.

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
