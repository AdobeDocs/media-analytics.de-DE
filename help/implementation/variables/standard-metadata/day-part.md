---
title: Teil des Tages
description: Legen Sie die Tageszeit (Morgen, Nachmittag, Primetime, Late Night) fest, zu der der Inhalt gesendet oder wiedergegeben wurde.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 7%

---


# Teil des Tages

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable &quot;**Teil“**. Siehe [Teil Tag](/help/reporting/dimensions/day-part.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable für den Tagesabschnitt ist der Behälter für die Tageszeit, in dem der Inhalt gesendet oder wiedergegeben wurde (z. B. `"Morning"`, `"Afternoon"`, `"Primetime"` oder `"Late Night"`). Jede Zeichenfolge wird akzeptiert. Damit können Sie die Interaktion über Tagesbereiche hinweg unabhängig von der lokalen Zeitzone des Betrachters vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.dayPart` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.dayPart` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`dayPart` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        dayPart: "Primetime"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie den Teil des Tages als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.DAY_PART`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie den Teil des Tages als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.DAY_PART`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Verwenden Sie `createMediaSession`, um `dayPart` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "dayPart": "Primetime"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `dayPart` in `xdm.mediaCollection.sessionDetails` auf:

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
          "dayPart": "Primetime"
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

Übergeben Sie den Teil des Tages im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.DayPart`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.DayPart] = "Primetime";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.VideoMetadataKeys.DAY_PART` , um den Day-Teil in der `StandardMediaMetadata`-Eigenschaft des Medienobjekts festzulegen, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "Primetime";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Verwenden Sie `MEDIA_VideoMetadataKeyDAY_PART` , um den Day-Teil in den Standard-Metadaten des Medienobjekts festzulegen, bevor Sie `mediaTrackSessionStart` aufrufen:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyDAY_PART] = "Primetime"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`media.dayPart` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.dayPart": "Primetime"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
