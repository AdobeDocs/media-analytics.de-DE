---
title: Genre
description: Legen Sie das Inhaltsgenre als kommagetrennte Zeichenfolge fest. Inhalte mit mehreren Genres werden in Berichten auf mehrere Zeileneinträge aufgeteilt.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 7%

---


# Genre

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Genre**behandelt. Siehe [Genre](/help/reporting/dimensions/genre.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Genre-Variable ist das Inhalts-Genre, wie es vom Produzenten definiert wurde (z. B. `"Drama"`, `"Comedy"` oder `"Drama,Action"`). Mehrere Werte durch Komma trennen, wenn der Inhalt für mehr als ein Genre passt. In Berichten teilt die Listenvariable jeden Wert in einen separaten Zeileneintrag auf, wobei jeder Zeileneintrag dieselbe Metrikgewichtung erhält.

>[!NOTE]
>
>In der Reporting-Pipeline wird der Genre-Wert als `xdm.mediaReporting.sessionDetails.genreList` (ein Listenfeld) verfügbar gemacht. Der Pfad der älteren `xdm.mediaReporting.sessionDetails.genre` bleibt funktionsfähig, wird jedoch `genreList` empfohlen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.genre` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.genre` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`genre` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie die Genre-Zeichenfolge als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.GENRE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie die Genre-Zeichenfolge als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.GENRE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Verwenden Sie `createMediaSession`, um `genre` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `genre` in `xdm.mediaCollection.sessionDetails` auf:

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
          "genre": "Drama,Action"
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

Übergeben Sie das Genre im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.Genre`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.VideoMetadataKeys.GENRE` , um das Genre in der `StandardMediaMetadata`-Eigenschaft des Medienobjekts festzulegen, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "Drama,Action";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Verwenden Sie `MEDIA_VideoMetadataKeyGENRE` , um das Genre in den Standardmetadaten des Medienobjekts festzulegen, bevor Sie `mediaTrackSessionStart` aufrufen:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyGENRE] = "Drama,Action"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`media.genre` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
