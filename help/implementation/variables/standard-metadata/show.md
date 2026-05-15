---
title: Serie
description: Legen Sie den Anzeigenamen für Videoinhalte fest, die Teil einer Serie sind, sodass Episoden in Berichten zu einem einzigen Programm zusammengefasst werden.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 13%

---


# Serie

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Anzeigen**behandelt. Siehe [Anzeigen](/help/reporting/dimensions/show.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable show ist der Name des Programms oder der Serie (z. B. `"Blinding Light"` oder `"Coastline Mysteries"`). Legen Sie sie für jede Sitzung fest, deren Inhalt zu einer Serie gehört, sodass Episoden über mehrere Jahreszeiten hinweg in einem einzigen Zeileneintrag in der Dimension Anzeigen angezeigt werden. Legen Sie sie für einmalige Inhalte, die nicht Teil einer Serie sind, nicht fest.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.show` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.show` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Web SDK

`show` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        show: "Blinding Light"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Anzeigenamen als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.SHOW`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `show` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "show": "Blinding Light"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `show` in `mediaCollection.sessionDetails` auf:

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
          "show": "Blinding Light"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Anzeigenamen mithilfe von `ADB.Media.VideoMetadataKeys.Show` an das `contextData`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Show] = "Blinding Light";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.show` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.show": "Blinding Light"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
