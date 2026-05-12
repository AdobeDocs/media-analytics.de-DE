---
title: Element-ID
description: Legen Sie die Asset-ID fest, eine stabile Branchenkennung für das Medien-Asset, wie z. B. eine EIDR- oder TMS/Gracenote-ID.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 13%

---


# Element-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Asset-ID**behandelt. Siehe [Asset-ID](/help/reporting/dimensions/asset-id.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Asset-ID-Variable ist die eindeutige Kennung für das zugrunde liegende Medien-Asset (z. B. eine Folge-ID, eine Film-ID oder eine Live-Ereignis-ID). In der Regel von Metadatenbehörden wie EIDR, TMS/Gracenote oder Rovi bezogen, aber auch proprietäre oder interne IDs werden akzeptiert. Verwenden Sie diese Option, wenn Sie die Interaktion zwischen Verteilungsplattformen vergleichen müssen, die demselben zugrunde liegenden Asset möglicherweise unterschiedliche Inhalts-IDs zuweisen.

>[!NOTE]
>
>Das XDM-Sammlungsfeld verwendet `ID` in Großbuchstaben: `assetID`.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.asset` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Erforderlich** | Nein |
| **Gesendet mit** | Sitzungsbeginn, Sitzungsabschluss |

## Web SDK

`assetID` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Asset-ID als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.ASSET_ID`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `assetID` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `assetID` in `mediaCollection.sessionDetails` auf:

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
          "assetID": "89745363"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Asset-ID im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.AssetId`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.assetId` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
