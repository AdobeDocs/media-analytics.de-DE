---
title: MVPD
description: Legen Sie den Multichannel Video Programming Distributor fest, wenn sich der Anwender über Adobe Pass authentifiziert.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 8%

---


# MVPD

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **MVPD**&#x200B;behandelt. Siehe [MVPD](/help/reporting/dimensions/mvpd.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die MVPD-Variable (Multi-Channel Video Programming Distributor) ist der Kabel-, Satelliten- oder Virtual-MVPD-Provider, über den sich der Benutzer authentifiziert hat (z. B. `"Comcast"`, `"DirecTV"` oder `"YouTubeTV"`). Legen Sie sie fest, wenn Inhalte hinter der Adobe Pass- oder TV-Everywhere-Authentifizierung erfasst werden. Koppeln Sie mit [Autorisiert](/help/implementation/variables/standard-metadata/authorized.md), um zu verfolgen, welche Sitzungen die Authentifizierung abgeschlossen haben.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.pass.mvpd` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.pass.mvpd` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`mvpd` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie die MVPD als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.MVPD`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie die MVPD als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.MVPD`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Verwenden Sie `createMediaSession`, um `mvpd` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `mvpd` in `xdm.mediaCollection.sessionDetails` auf:

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
          "mvpd": "Comcast"
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

Übergeben Sie die MVPD im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.MVPD`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.VideoMetadataKeys.MVPD` , um den MVPD in der `StandardMediaMetadata`-Eigenschaft des Medienobjekts festzulegen, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "Comcast";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Verwenden Sie `MEDIA_VideoMetadataKeyMVPD` , um den MVPD in den Standardmetadaten des Medienobjekts festzulegen, bevor Sie `mediaTrackSessionStart` aufrufen:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyMVPD] = "Comcast"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`media.pass.mvpd` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
