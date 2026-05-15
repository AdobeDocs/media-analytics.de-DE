---
title: Platzierungs-ID
description: Legen Sie die Platzierungs-ID für jede Anzeige fest, um Ausbrüche nach Anzeigenplatzierung zu ermöglichen.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 17%

---


# Platzierungs-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Platzierungs-ID**behandelt. Siehe [Platzierungs-ID](/help/reporting/dimensions/placement-id.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Platzierungs-ID-Variable identifiziert die Anzeigenplatzierung (normalerweise ein Slot oder eine Zone, die in Ihrer Anzeigenserverplattform definiert ist).

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.placement` |
| **XDM-Sammlungsfeld** | [`mediaCollection.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.ad.placement` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Anzeigenstart](/help/implementation/events/ads/ad-start.md), Anzeigenschluss |

## Web SDK

`placementID` in `mediaCollection.advertisingDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        placementID: "placement-12"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Platzierungs-ID als Metadatenschlüssel im HashMap-Argument an `trackEvent(AdStart)`. Verwenden Sie `MediaConstants.AdMetadataKeys.PLACEMENT_ID`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Legen Sie `placementID` in `mediaCollection.advertisingDetails` fest, wenn Sie `sendMediaEvent` für `media.adStart` aufrufen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "placementID": "placement-12"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) mit `placementID` in `mediaCollection.advertisingDetails` auf:

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
          "placementID": "placement-12"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Platzierungs-ID im `contextData`-Objekt mithilfe von `ADB.Media.AdMetadataKeys.PlacementId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.PlacementId] = "placement-12";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Mediensammlungs-API

`media.ad.placementId` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.placementId": "placement-12"
  }
}
```

Die vollständige Anfragestruktur [ Sie in der ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
