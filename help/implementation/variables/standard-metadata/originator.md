---
title: Urheber
description: Legen Sie den Ersteller oder das Produktionsstudio des Inhalts fest.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 16%

---


# Urheber

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Originator**behandelt. Siehe [Urheber](/help/reporting/dimensions/originator.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die originator-Variable ist der Ersteller oder das Produktionsstudio des Inhalts (z. B. `"Warner Brothers"`, `"Sony"` oder `"Disney"`). Verwenden Sie sie, um die Interaktion zwischen Inhaltsinhabern oder Rechteinhabern zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.originator` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.originator`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.originator` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`originator` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        originator: "Warner Brothers"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Urheber als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.ORIGINATOR`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `originator` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "originator": "Warner Brothers"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `originator` in `mediaCollection.sessionDetails` auf:

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
          "originator": "Warner Brothers"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Urheber im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.Originator`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Originator] = "Warner Brothers";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.originator` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.originator": "Warner Brothers"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
