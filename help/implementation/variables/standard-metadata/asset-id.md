---
title: Element-ID
description: Legen Sie die Asset-ID fest, eine stabile Branchenkennung für das Medien-Asset, wie z. B. eine EIDR- oder TMS/Gracenote-ID.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 8%

---


# Element-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Asset-ID**&#x200B;behandelt. Siehe [Asset-ID](/help/reporting/dimensions/asset-id.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Asset-ID-Variable ist die eindeutige Kennung für das zugrunde liegende Medien-Asset (z. B. eine Folge-ID, eine Film-ID oder eine Live-Ereignis-ID). In der Regel von Metadatenbehörden wie EIDR, TMS/Gracenote oder Rovi bezogen, aber auch proprietäre oder interne IDs werden akzeptiert. Verwenden Sie diese Option, wenn Sie die Interaktion zwischen Verteilungsplattformen vergleichen müssen, die demselben zugrunde liegenden Asset möglicherweise unterschiedliche Inhalts-IDs zuweisen.

>[!NOTE]
>
>Das XDM-Sammlungsfeld verwendet `ID` in Großbuchstaben: `assetID`.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.asset` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.asset` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`assetID` in `xdm.mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

>[!TAB iOS]

Übergeben Sie die Asset-ID als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.ASSET_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Übergeben Sie die Asset-ID als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.ASSET_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

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

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `assetID` in `xdm.mediaCollection.sessionDetails` auf:

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Übergeben Sie die Asset-ID im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.AssetId`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Verwenden Sie `ADBMobile.media.VideoMetadataKeys.ASSET_ID` , um die Asset-ID in der `StandardMediaMetadata`-Eigenschaft des Medienobjekts festzulegen, bevor Sie `trackSessionStart` aufrufen:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.ASSET_ID] = "89745363";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

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

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
