---
title: Start der Werbeunterbrechung
description: Signalisieren Sie den Beginn einer Werbeunterbrechung (eine Sequenz aus einer oder mehreren Anzeigen).
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 13%

---


# Start der Werbeunterbrechung

Das Start-Ereignis für die Werbeunterbrechung signalisiert den Beginn einer Werbeunterbrechung. Eine Werbeunterbrechung ist eine Sequenz aus einer oder mehreren Anzeigen. Jedes `adStart`-, `adComplete`- und `adSkip`-Ereignis muss zwischen einem `adBreakStart`- und `adBreakComplete`-Paar auftreten, auch wenn eine einzelne Anzeige abgespielt wird.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: Keine

>[!IMPORTANT]
>
>Anzeigenereignisse (`adStart`, `adComplete`, `adSkip`) werden ohne `adBreakStart` und `adBreakComplete` Buchstützen ignoriert. Ohne sie wird die Anzeigendauer der Hauptinhaltsdauer zugeordnet, was sich auf aggregierte Berichtsdaten auswirkt.

## Web SDK

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

## Mobile SDK

Übergeben Sie den Namen, die Position und die Startzeit der Werbeunterbrechung an `createAdBreakObject` und rufen Sie dann `trackEvent` auf.

**iOS (SWIFT)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

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

## Media Edge-API

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

## Medien-SDK

Übergeben Sie den Namen, die Position und die Startzeit der Werbeunterbrechung an `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Mediensammlungs-API

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
