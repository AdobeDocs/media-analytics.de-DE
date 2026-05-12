---
title: Erstes digitales Datum
description: Legen Sie das Datum fest, an dem der Inhalt erstmals auf einer digitalen Plattform ausgestrahlt wird. Adobe empfiehlt das Format JJJJ-MM-TT.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---


# Erstes digitales Datum

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Erstes digitales Datum**behandelt. Siehe [Erstes digitales Datum](/help/reporting/dimensions/first-digital-date.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die erste digitale Datumsvariable ist das Datum, an dem der Inhalt auf einer digitalen Plattform erstmals ausgestrahlt wird. Jedes Datumsformat wird akzeptiert, Adobe empfiehlt jedoch aus Konsistenzgründen die `YYYY-MM-DD`. Verwenden Sie neben [Erstes Sendedatum](/help/implementation/variables/standard-metadata/first-air-date.md), um den digitalen Veröffentlichungszeitpunkt mit der Originalsendung zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.digitalDate` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Erforderlich** | Nein |
| **Gesendet mit** | Sitzungsbeginn, Sitzungsabschluss |

## Web SDK

`firstDigitalDate` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie das erste digitale Datum als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `firstDigitalDate` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `firstDigitalDate` in `mediaCollection.sessionDetails` auf:

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
          "firstDigitalDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie das erste digitale Datum in das `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.FirstDigitalDate`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.firstDigitalDate` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
