---
title: Sendungstyp
description: Identifizieren Sie das Inhaltsformat (vollständige Folge, Vorschau, Clip oder andere) mithilfe eines Zeichenfolgen-Ganzzahlcodes.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 13%

---


# Sendungstyp

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Typ anzeigen**&#x200B;behandelt. Siehe [Sendungstyp](/help/reporting/dimensions/show-type.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable vom Typ „show“ identifiziert das Inhaltsformat mithilfe eines Zeichenfolgen-Ganzzahlcodes:

- `"0"`: Full Episode
- `"1"`: Vorschau oder Trailer
- `"2"`: Clip
- `"3"`: Sonstiges

Verwenden Sie diese Option, um bei der Messung der Interaktion die Anzeige eines vollständigen Programms von kurzen Inhalten wie Trailern und Clips zu trennen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.type` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.showType`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.type` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`showType` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        showType: "0"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Sendungstyp als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.SHOW_TYPE`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `showType` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "showType": "0"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `showType` in `mediaCollection.sessionDetails` auf:

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
          "showType": "0"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Sendungstyp mithilfe von `ADB.Media.VideoMetadataKeys.ShowType` an das `contextData`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.ShowType] = "0";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.showType` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.showType": "0"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
