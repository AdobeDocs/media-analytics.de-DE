---
title: Künstler
description: Den Namen des Interpreten für den Audioinhalt festlegen.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 9%

---


# Künstler

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Artist**&#x200B;behandelt. Siehe [Interpret](/help/reporting/dimensions/artist.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable artist ist der Name des Interpreten, der Audioinhalte ausführt (z. B. `"Crested Larks"`). Verwenden Sie es für Musik- oder Podcast-Sitzungen, um die Interaktion eines Interpreten zu unterbrechen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.artist` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.artist`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.artist` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`artist` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        artist: "Crested Larks"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie den Namen des Interpreten als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.AudioMetadataKeys.ARTIST`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie den Namen des Interpreten als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.AudioMetadataKeys.ARTIST`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Verwenden Sie `createMediaSession`, um `artist` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "artist": "Crested Larks"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `artist` in `xdm.mediaCollection.sessionDetails` auf:

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
          "artist": "Crested Larks"
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

Übergeben Sie den Interpreten im `contextData`-Objekt mithilfe von `ADB.Media.AudioMetadataKeys.Artist`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Artist] = "Crested Larks";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.AudioMetadataKeys.ARTIST` , um den Namen des Interpreten in der `StandardMediaMetadata`-Eigenschaft des Medienobjekts festzulegen, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = "Crested Larks";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Verwenden Sie `MEDIA_AudioMetadataKeyARTIST`, um den Namen des Interpreten in den Standardmetadaten des Medienobjekts festzulegen, bevor Sie `mediaTrackSessionStart` aufrufen:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeyARTIST] = "Crested Larks"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`media.artist` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.artist": "Crested Larks"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
