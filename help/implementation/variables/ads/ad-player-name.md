---
title: Player-Namen hinzufügen
description: Den Namen des Players festlegen, der Anzeigen rendert. Der Anzeigen-Player kann sich vom Hauptinhalt-Player unterscheiden.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 11%

---


# Player-Namen hinzufügen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Ad-Player-Name**&#x200B;behandelt. Siehe [Player-Name hinzufügen](/help/reporting/dimensions/ad-player-name.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „Anzeigenplayer-Name“ gibt an, welcher Player jede Anzeige gerendert hat (z. B. `"Freewheel"`, `"Google IMA"`). Der Anzeigen-Player kann sich vom Hauptinhalt-Player unterscheiden, wenn Anzeigen von einem Server-seitigen Anzeigeneinfüge-Service zusammengefügt werden. Verwenden Sie diese Variable, um die Qualität und den Abschluss über Anzeigenbereitstellungs-Stacks hinweg zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.playerName` |
| **XDM-Sammlungsfeld** | [`mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.ad.playerName` |
| **Erforderlich** | Ja |
| **Gesendet mit** | [Anzeigenstart](/help/implementation/events/ads/ad-start.md), Anzeigenschluss |

## Web SDK

`playerName` in `mediaCollection.advertisingDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie den Namen des Anzeigen-Players als `MediaConstants.AdMetadataKeys.AD_PLAYER` Schlüssel im Metadaten-HashMap-Argument an `trackEvent(AdStart)`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Legen Sie `playerName` in `mediaCollection.advertisingDetails` fest, wenn Sie `sendMediaEvent` für `media.adStart` aufrufen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) mit `playerName` in `mediaCollection.advertisingDetails` auf:

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
          "podPosition": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Namen des Anzeigen-Players im `contextData`-Objekt mithilfe von `ADB.Media.AdMetadataKeys.AdPlayer`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Mediensammlungs-API

Fügen Sie `media.ad.playerName` in das `params` Ihrer `adStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
