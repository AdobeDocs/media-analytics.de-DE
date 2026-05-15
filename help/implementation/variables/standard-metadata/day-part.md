---
title: Teil des Tages
description: Legen Sie die Tageszeit (Morgen, Nachmittag, Primetime, Late Night) fest, zu der der Inhalt gesendet oder wiedergegeben wurde.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# Teil des Tages

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable &quot;**Teil“**. Siehe [Teil Tag](/help/reporting/dimensions/day-part.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable für den Tagesabschnitt ist der Behälter für die Tageszeit, in dem der Inhalt gesendet oder wiedergegeben wurde (z. B. `"Morning"`, `"Afternoon"`, `"Primetime"` oder `"Late Night"`). Jede Zeichenfolge wird akzeptiert. Damit können Sie die Interaktion über Tagesbereiche hinweg unabhängig von der lokalen Zeitzone des Betrachters vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.dayPart` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.dayPart`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.dayPart` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`dayPart` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

## Mobile SDK

Übergeben Sie den Teil des Tages als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.DAY_PART`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `dayPart` in `mediaCollection.sessionDetails` auf:

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

## Medien-SDK

Übergeben Sie den Teil des Tages im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.DayPart`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.DayPart] = "Primetime";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

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

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
