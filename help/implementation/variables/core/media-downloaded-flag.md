---
title: Markierung für heruntergeladene Medien
description: Markieren Sie eine Sitzung als heruntergeladene Offline-Wiedergabe, damit sie getrennt von gestreamten Sitzungen gemeldet wird.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 5%
---

# Markierung für heruntergeladene Medien

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Media Downloaded Flag**behandelt. Siehe [Medien heruntergeladen](/help/reporting/dimensions/media-downloaded-flag.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Markierung für heruntergeladene Medien gibt an, dass eine Sitzung die Wiedergabe zuvor heruntergeladener Offline-Inhalte und nicht einen Live-Stream aus dem Internet ist. Legen Sie diese beim Initialisieren des Trackers (Mobile SDK) fest oder fügen Sie ihn in die `sessionStart`-Payload ein (Edge / Mediensammlungs-API). Verwenden Sie dieses Flag, um die Offline-Wiedergabe von Streaming-Sitzungen in Berichten zu trennen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.downloaded` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.downloaded` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Legen Sie `isDownloaded` beim Aufrufen von [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) auf `true` in `xdm.mediaCollection.sessionDetails` fest:

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
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Setzen Sie beim Erstellen des Trackers mithilfe von `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT` das Flag für heruntergeladene Inhalte in der Tracker-Konfiguration.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

Setzen Sie beim Erstellen des Trackers mithilfe von `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT` das Flag für heruntergeladene Inhalte in der Tracker-Konfiguration.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

Legen Sie `isDownloaded` beim Aufrufen von `createMediaSession` auf `true` in `xdm.mediaCollection.sessionDetails` fest:

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
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den Endpunkt [HERUNTERGELADEN](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded) auf, nachdem das Gerät online zurückgekehrt ist, und stapeln Sie die vollständige Offline-Sitzung in `mediaDownloadedEvents`. Adobe setzt `isDownloaded` automatisch auf `true` und weist eine Sitzungs-ID zu. Sie dürfen keines von beiden in die Payload einschließen.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
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
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Legen Sie `downloadedContent` auf `ADB.MediaConfig` fest, bevor Sie den Tracker erstellen:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

Legen Sie `MediaDownloaded` für das Medieninformationsobjekt fest, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaDownloaded] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Das Tracking heruntergeladener Inhalte ist in der Roku 2.x-SDK nicht verfügbar. Verwenden Sie zum Melden heruntergeladener Medienwiedergaben die [Roku Edge SDK](/help/implementation/edge/roku.md) oder die [Mediensammlungs-API](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/implementation).

>[!TAB Media Collection API]

Fügen Sie `media.downloaded` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
