---
title: Name des Inhalts-Players
description: Legen Sie den Player-Namen fest, um zu identifizieren, welcher Player den Inhalt gerendert hat.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 6%

---


# Name des Inhalts-Players

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Content Player Name**&#x200B;behandelt. Siehe [Name des Content](/help/reporting/dimensions/content-player-name.md)Players“ für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „Name des Inhalts-Players“ gibt an, welcher Player den Inhalt gerendert hat (z. B. `HTML5 Player`, `Brightcove` oder `Roku Player`). Sie ist für alle Implementierungen von Streaming-Medien erforderlich und muss beim Sitzungsstart festgelegt werden. Der Wert wird in der Dimension Name des Inhalts-Players verwendet, um die Interaktion und Qualität zwischen Playern in derselben Eigenschaft zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.playerName` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.playerName` |
| **Erforderlich** | Ja |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`playerName` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

Legen Sie den Player-Namen über die Tracker-Konfiguration fest, wenn Sie den Tracker mithilfe von `MediaConstants.TrackerConfig.PLAYER_NAME` erstellen. Der Player-Name ist nicht Teil des Medienobjekts.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

Legen Sie den Player-Namen über die Tracker-Konfiguration fest, wenn Sie den Tracker mithilfe von `MediaConstants.TrackerConfig.PLAYER_NAME` erstellen. Der Player-Name ist nicht Teil des Medienobjekts.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

`playerName` in `xdm.mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

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

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `playerName` in `xdm.mediaCollection.sessionDetails` auf:

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

Legen Sie den Player-Namen auf `ADB.MediaConfig` fest, bevor Sie den Tracker erstellen:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

Übergeben Sie den Player-Namen als Standard-Metadatenschlüssel beim Aufruf von `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.playerName": "Chromecast Player" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Roku 2.x]

`playerName` Sie im `mediaHeartbeat` Abschnitt von `ADBMobileConfig.json`. Der Player-Name ist ein Konfigurationswert, kein Wert pro Sitzung:

```json
"mediaHeartbeat": {
  "playerName": "Roku Player"
}
```

>[!TAB Media Collection API]

Fügen Sie `media.playerName` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
