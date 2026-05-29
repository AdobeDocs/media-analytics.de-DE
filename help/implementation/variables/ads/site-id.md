---
title: Site-ID
description: Legen Sie die Anzeigenstandort-ID für jede Anzeige fest, um Ausbrüche nach Anzeigenplatzierungs-Site zu ermöglichen.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 11%

---


# Site-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Site-ID**&#x200B;behandelt. Siehe [Site-ID](/help/reporting/dimensions/site-id.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Site-ID-Variable identifiziert die Anzeigen-Site. Jeder Zeichenfolgenwert (normalerweise eine ID aus Ihrer Ad-Server-Plattform) ist zulässig.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.site` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.ad.site` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Anzeigenstart](/help/implementation/events/ads/ad-start.md), Anzeigenschluss |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`siteID` in `xdm.mediaCollection.advertisingDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

>[!TAB iOS]

Übergeben Sie die Site-ID als Metadatenschlüssel im HashMap-Argument an `trackEvent(AdStart)`. Verwenden Sie `MediaConstants.AdMetadataKeys.SITE_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie die Site-ID als Metadatenschlüssel im HashMap-Argument an `trackEvent(AdStart)`. Verwenden Sie `MediaConstants.AdMetadataKeys.SITE_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

Legen Sie `siteID` in `xdm.mediaCollection.advertisingDetails` fest, wenn Sie `sendMediaEvent` für `media.adStart` aufrufen:

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

>[!TAB Media Edge-API]

Rufen Sie den Endpunkt [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) mit `siteID` in `xdm.mediaCollection.advertisingDetails` auf:

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Übergeben Sie die Site-ID im `contextData`-Objekt mithilfe von `ADB.Media.AdMetadataKeys.SiteId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.SiteId] = "site-42";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Legen Sie die Site-ID mithilfe von `ADBMobile.media.AdMetadataKeys.SITE_ID` im Standard-Anzeigenmetadaten-Objekt fest:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "site-42";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
