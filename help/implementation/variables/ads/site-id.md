---
title: Site-ID
description: Legen Sie die Anzeigenstandort-ID für jede Anzeige fest, um Ausbrüche nach Anzeigenplatzierungs-Site zu ermöglichen.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 17%

---


# Site-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Site-ID**&#x200B;behandelt. Siehe [Site-ID](/help/reporting/dimensions/site-id.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Site-ID-Variable identifiziert die Anzeigen-Site. Jeder Zeichenfolgenwert (normalerweise eine ID aus Ihrer Ad-Server-Plattform) ist zulässig.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.site` |
| **XDM-Sammlungsfeld** | [`mediaCollection.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.ad.site` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Anzeigenstart](/help/implementation/events/ads/ad-start.md), Anzeigenschluss |

## Web SDK

`siteID` in `mediaCollection.advertisingDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        siteID: "site-42"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Site-ID als Metadatenschlüssel im HashMap-Argument an `trackEvent(AdStart)`. Verwenden Sie `MediaConstants.AdMetadataKeys.SITE_ID`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Legen Sie `siteID` in `mediaCollection.advertisingDetails` fest, wenn Sie `sendMediaEvent` für `media.adStart` aufrufen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "siteID": "site-42"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) mit `siteID` in `mediaCollection.advertisingDetails` auf:

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
          "siteID": "site-42"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Site-ID im `contextData`-Objekt mithilfe von `ADB.Media.AdMetadataKeys.SiteId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.SiteId] = "site-42";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Mediensammlungs-API

`media.ad.siteId` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.siteId": "site-42"
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
