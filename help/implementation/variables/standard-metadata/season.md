---
title: Staffel
description: Legen Sie die Saisonnummer für episodische Inhalte fest, damit die Interaktion nach Saison unterbrochen werden kann.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 9%

---


# Staffel

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Season**&#x200B;behandelt. Siehe [Staffel](/help/reporting/dimensions/season.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Staffelvariable ist die Staffelnummer für die Sendung (normalerweise eine ganze Zahl wie `"2"`). Legen Sie ihn für Inhalte fest, die Teil einer Serie sind, damit die Interaktion nach Saison unterbrochen werden kann. Kombinieren Sie mit [Sendung](/help/implementation/variables/standard-metadata/show.md) und [Episode](/help/implementation/variables/standard-metadata/episode.md) für vollen episodischen Kontext.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.season` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.season` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`season` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        season: "2"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie die Jahreszeit als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.SEASON`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie die Jahreszeit als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.SEASON`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Verwenden Sie `createMediaSession`, um `season` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "season": "2"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `season` in `xdm.mediaCollection.sessionDetails` auf:

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
          "season": "2"
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

Übergeben Sie die Saison im `contextData` mit `ADB.Media.VideoMetadataKeys.Season`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Season] = "2";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.VideoMetadataKeys.SEASON`, um die Saisonnummer in der `StandardMediaMetadata`-Eigenschaft des Medienobjekts festzulegen, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "2";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

`media.season` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.season": "2"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
