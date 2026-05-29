---
title: Anzeigenstart
description: Signal, dass die Wiedergabe einer einzelnen Anzeige begonnen hat.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 8%

---


# Anzeigenstart

Das Anzeigenstartereignis signalisiert, dass die Wiedergabe einer einzelnen Anzeige begonnen hat. Sie muss innerhalb eines [Anzeigenunterbrechungsstart](ad-break-start.md)/[Anzeigenunterbrechung abgeschlossen](ad-break-complete.md)-Paars erfolgen.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Start der Werbeunterbrechung](ad-break-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Anzeigenstarts]](/help/reporting/metrics/ad-starts.md)

>[!IMPORTANT]
>
>Dieses Ereignis muss von `adBreakStart` und `adBreakComplete` Buchstützen umgeben sein, selbst wenn eine einzige Anzeige abgespielt wird. Ohne diese Buchstützen werden Anzeigenereignisse ignoriert und die Anzeigendauer wird als Hauptinhaltsdauer gezählt.

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.adStart"` und den erforderlichen `advertisingDetails` auf:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie den Anzeigenamen, die ID, die Pod-Position und die Länge an `createAdObject` und rufen Sie dann `trackEvent` auf.

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie den Anzeigenamen, die ID, die Pod-Position und die Länge an `createAdObject` und rufen Sie dann `trackEvent` auf.

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0,
                                    15)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku]

Rufen Sie `sendMediaEvent` mit `eventType: "media.adStart"` und den erforderlichen `advertisingDetails` auf:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)-Endpunkt mit dem erforderlichen `advertisingDetails` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Übergeben Sie Anzeigenamen, ID, Position und Länge an `ADB.Media.createAdObject`:

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, null);
```

>[!TAB Chromecast]

Übergeben Sie Anzeigenamen, ID, Position und Länge an `ADBMobile.media.createAdObject`:

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Media Collection API]

Senden eines `adStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125",
    "media.ad.name": "Ford F-150",
    "media.ad.length": 15,
    "media.ad.podPosition": 0
  }
}
```

>[!ENDTABS]
