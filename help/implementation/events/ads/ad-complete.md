---
title: Hinzufügen abgeschlossen
description: Signal, dass die Wiedergabe einer einzelnen Anzeige abgeschlossen ist.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 15%

---


# Hinzufügen abgeschlossen

Das Ereignis „Anzeige abgeschlossen“ signalisiert, dass die Wiedergabe einer einzelnen Anzeige abgeschlossen ist. Senden Sie es, nachdem die Anzeige bis zum Ende abgespielt wurde. Wenn der Viewer die Anzeige überspringt, senden Sie stattdessen [Anzeige überspringen](ad-skip.md).

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Anzeigenunterbrechungsstart](ad-break-start.md), [Anzeigenstart](ad-start.md)
* **Zugeordnete Metrik**: [Anzeige abgeschlossen](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Dieses Ereignis muss von `adBreakStart` und `adBreakComplete` Buchstützen umgeben sein, selbst wenn eine einzige Anzeige abgespielt wird. Ohne diese Buchstützen werden Anzeigenereignisse ignoriert und die Anzeigendauer wird als Hauptinhaltsdauer gezählt.

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.adComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackEvent` mit dem `AdComplete` Ereignistyp auf.

**iOS (SWIFT)**

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.adComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete) auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackEvent` mit dem `AdComplete` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

## Mediensammlungs-API

Senden eines `adComplete` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```
