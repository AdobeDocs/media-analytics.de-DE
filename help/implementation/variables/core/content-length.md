---
title: Länge des Inhalts
description: Legen Sie die Inhaltslänge in Sekunden beim Sitzungsstart fest. Sie steuert Fortschrittsmarken und den Zielgruppendurchschnitt pro Minute.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 12%

---


# Länge des Inhalts

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Content length**&#x200B;behandelt. Siehe [Inhaltslänge](/help/reporting/dimensions/content-length.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Inhaltslängenvariable ist die Gesamtdauer des Inhalts in Sekunden. Sie ist für alle Implementierungen von Streaming-Medien erforderlich und muss beim Sitzungsstart festgelegt werden. Die Inhaltslänge bestimmt mehrere im Backend berechnete Metriken, einschließlich Fortschrittsmarken (10/25/50/75/95 %) und Zielgruppendurchschnitt pro Minute. Wenn die Inhaltslänge nicht festgelegt ist oder nicht größer als null ist, werden diese Metriken nicht erstellt. Verwenden Sie für Live-Streams mit unbekannter Dauer `86400` (24 Stunden).

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.length` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.length`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Erforderlich** | Ja |
| **Gesendet mit** | Sitzungsbeginn, Sitzungsabschluss |

## Web SDK

`length` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

Übergeben Sie die Inhaltslänge in Sekunden als `length` an `createMediaObject`.

**iOS (SWIFT)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

`length` in `mediaCollection.sessionDetails` festlegen, wenn `createMediaSession` aufgerufen wird:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
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

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `length` in `mediaCollection.sessionDetails` auf:

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

## Medien-SDK

Übergeben Sie die Inhaltslänge in Sekunden als drittes Argument für `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,                      // length in seconds
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.length` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.length": 128
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
