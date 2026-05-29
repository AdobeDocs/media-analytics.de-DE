---
title: Start der Werbeunterbrechung
description: Signalisieren Sie den Beginn einer Werbeunterbrechung (eine Sequenz aus einer oder mehreren Anzeigen).
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 7%

---


# Start der Werbeunterbrechung

Das Start-Ereignis für die Werbeunterbrechung signalisiert den Beginn einer Werbeunterbrechung. Eine Werbeunterbrechung ist eine Sequenz aus einer oder mehreren Anzeigen. Jedes `adStart`-, `adComplete`- und `adSkip`-Ereignis muss zwischen einem `adBreakStart`- und `adBreakComplete`-Paar auftreten, auch wenn eine einzelne Anzeige abgespielt wird.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: Keine

>[!IMPORTANT]
>
>Anzeigenereignisse (`adStart`, `adComplete`, `adSkip`) werden ohne `adBreakStart` und `adBreakComplete` Buchstützen ignoriert. Ohne sie wird die Anzeigendauer der Hauptinhaltsdauer zugeordnet, was sich auf aggregierte Berichtsdaten auswirkt.

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.adBreakStart"` und den erforderlichen `advertisingPodDetails` auf:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie den Namen, die Position und die Startzeit der Werbeunterbrechung an `createAdBreakObject` und rufen Sie dann `trackEvent` auf.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie den Namen, die Position und die Startzeit der Werbeunterbrechung an `createAdBreakObject` und rufen Sie dann `trackEvent` auf.

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku]

Rufen Sie `sendMediaEvent` mit `eventType: "media.adBreakStart"` und den erforderlichen `advertisingPodDetails` auf:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart)-Endpunkt mit dem erforderlichen `advertisingPodDetails` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingPodDetails": {
          "index": 0,
          "offset": 0
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

Übergeben Sie den Namen, die Position und die Startzeit der Werbeunterbrechung an `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

Übergeben Sie den Namen, die Position und die Startzeit der Werbeunterbrechung an `ADBMobile.media.createAdBreakObject`:

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Media Collection API]

Senden eines `adBreakStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll",
    "media.ad.podIndex": 1,
    "media.ad.podSecond": 0
  }
}
```

>[!ENDTABS]
