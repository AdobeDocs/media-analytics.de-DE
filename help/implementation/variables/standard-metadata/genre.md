---
title: Genre
description: Legen Sie das Inhaltsgenre als kommagetrennte Zeichenfolge fest. Inhalte mit mehreren Genres werden in Berichten auf mehrere Zeileneinträge aufgeteilt.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 13%

---


# Genre

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Genre**behandelt. Siehe [Genre](/help/reporting/dimensions/genre.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Genre-Variable ist das Inhalts-Genre, wie es vom Produzenten definiert wurde (z. B. `"Drama"`, `"Comedy"` oder `"Drama,Action"`). Mehrere Werte durch Komma trennen, wenn der Inhalt für mehr als ein Genre passt. In Berichten teilt die Listenvariable jeden Wert in einen separaten Zeileneintrag auf, wobei jeder Zeileneintrag dieselbe Metrikgewichtung erhält.

>[!NOTE]
>
>In der Reporting-Pipeline wird der Genre-Wert als `mediaReporting.sessionDetails.genreList` (ein Listenfeld) verfügbar gemacht. Der Pfad der älteren `mediaReporting.sessionDetails.genre` bleibt funktionsfähig, wird jedoch `genreList` empfohlen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.genre` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Erforderlich** | Nein |
| **Gesendet mit** | Sitzungsbeginn, Sitzungsabschluss |

## Web SDK

`genre` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

## Mobile SDK

Übergeben Sie die Genre-Zeichenfolge als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.GENRE`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `genre` in `mediaCollection.sessionDetails` auf:

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

## Medien-SDK

Übergeben Sie das Genre im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.Genre`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

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
