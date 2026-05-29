---
title: Sitzungsstart
description: Signalisieren Sie den Beginn einer Mediensitzung und erhalten Sie die Sitzungs-ID, die für alle nachfolgenden Ereignisse erforderlich ist.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 5%

---


# Sitzungsstart

Das Sitzungsstartereignis öffnet eine Medienverfolgungssitzung. Es muss das erste Ereignis sein, das für eine Wiedergabe gesendet wird. Die Antwort gibt eine Sitzungs-ID zurück, die alle nachfolgenden Ereignisse für dieselbe Sitzung enthalten müssen.

Eine Sitzung läuft automatisch ab **wenn für 10 Minuten keine Ereignisse empfangen werden** oder wenn **keine Abspielkopfbewegung für 30 Minuten“**. Wenn eine Sitzung abläuft, müssen Sie den Sitzungsstart erneut aufrufen, um eine neue Sitzungs-ID zu erhalten.

* **Voraussetzungen**: Keine; immer das erste Ereignis
* **Zugeordnete Metrik**: [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md)

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Rufen Sie `trackSessionStart` mit einem Medienobjekt und optionalen Metadaten auf.

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Rufen Sie `trackSessionStart` mit einem Medienobjekt und optionalen Metadaten auf.

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Rufen Sie `trackSessionStart` mit einem Medienobjekt auf, das mit `ADBMobile.media.createMediaObject` erstellt wurde:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "video-123",                        // name
  "video-id-123",                     // media ID
  128,                                // length (seconds)
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);

ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]

## Wiederaufnehmen einer Sitzung

Wenn Sie eine zuvor geschlossene Sitzung fortsetzen - z. B. nach einer geräteübergreifenden Übergabe oder nachdem die Anwendung den gespeicherten Wiedergabestatus wiederhergestellt hat -, setzen Sie das Resume-Flag beim Sitzungsstart. Dadurch wird Analytics [[!UICONTROL Inhaltswiederaufnahmen]](/help/reporting/metrics/content-resumes.md) anstelle von „Medienstarts[[!UICONTROL &#x200B; erhöht]](/help/reporting/metrics/media-starts.md).

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`hasResume: true` zu `sessionDetails` hinzufügen:

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
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Legen Sie den `resumed` Schlüssel des Medienobjekts fest, bevor Sie `trackSessionStart` aufrufen:

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

mediaObject[MediaConstants.MediaObjectKey.resumed] = true
tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Legen Sie den `RESUMED` Schlüssel des Medienobjekts fest, bevor Sie `trackSessionStart` aufrufen:

```kotlin
val mediaObject = Media.createMediaObject("video-123", "video-id-123", 128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

mediaObject[Media.MediaObjectKey.RESUMED] = true
tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku]

`"hasResume": true` zu `sessionDetails` hinzufügen:

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
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

`"hasResume": true` zu `sessionDetails` hinzufügen:

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
          "channel": "Sports",
          "hasResume": true
        },
        "playhead": 0
      }
    }
  }]
}'
```

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Legen Sie den `MediaResumed` auf das Medienobjekt fest:

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video
);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;
tracker.trackSessionStart(mediaObject, null);
```

>[!TAB Chromecast]

Legen Sie den `MediaResumed` auf das Medienobjekt fest:

```javascript
var mediaObject = ADBMobile.media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video
);

mediaObject[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaObject, null);
```

>[!TAB Media Collection API]

Fügen Sie `"media.resume": true` zum `params` hinzu:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123",
    "media.resume": true
  }
}
```

>[!ENDTABS]
