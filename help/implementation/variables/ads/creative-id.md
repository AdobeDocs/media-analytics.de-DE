---
title: Creative-ID
description: Legen Sie die Kreativ-ID für jede Anzeige fest.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 18%

---


# Creative-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Creative ID**&#x200B;behandelt. Siehe [Creative ID](/help/reporting/dimensions/creative-id.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „creative ID“ identifiziert die spezifische und kreative ID. Jeder Zeichenfolgenwert (normalerweise eine kreative ID aus Ihrer Ad-Server-Plattform) ist zulässig.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.creative` |
| **XDM-Sammlungsfeld** | [`mediaCollection.advertisingDetails.creativeID`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Erforderlich** | Nein |
| **Gesendet mit** | Anzeigenstart, Anzeigenschluss |

## Web SDK

`creativeID` in `mediaCollection.advertisingDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeID: "creative-987"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Kreativ-ID als Metadatenschlüssel im HashMap-Argument an `trackEvent(AdStart)`. Verwenden Sie `MediaConstants.AdMetadataKeys.CREATIVE_ID`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Legen Sie `creativeID` in `mediaCollection.advertisingDetails` fest, wenn Sie `sendMediaEvent` für `media.adStart` aufrufen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeID": "creative-987"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) mit `creativeID` in `mediaCollection.advertisingDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0,
          "creativeID": "creative-987"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Kreativ-ID im `contextData`-Objekt mithilfe von `ADB.Media.AdMetadataKeys.CreativeId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeId] = "creative-987";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Mediensammlungs-API

`media.ad.creativeId` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeId": "creative-987"
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
