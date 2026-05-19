---
title: Werbeunterbrechung abgeschlossen
description: Signal, dass alle Anzeigen in einer Werbeunterbrechung beendet sind.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 16%

---


# Werbeunterbrechung abgeschlossen

Das Ereignis „Anzeigenunterbrechung abgeschlossen“ signalisiert, dass alle Anzeigen in einer Anzeigenunterbrechung abgeschlossen (entweder abgeschlossen oder übersprungen) sind. Dadurch wird die durch „Start der Werbeunterbrechung[&#x200B; geöffnete Werbeunterbrechung &#x200B;](ad-break-start.md).

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Start der Werbeunterbrechung](ad-break-start.md)
* **Zugeordnete Metrik**: Keine

>[!IMPORTANT]
>
>Jeder `adBreakStart` muss einen passenden `adBreakComplete` haben. Ohne das schließende Bookend werden Anzeigenereignisse ignoriert und die Anzeigendauer wird dem Hauptinhalt zugeordnet.

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.adBreakComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackEvent` mit dem `AdBreakComplete` Ereignistyp auf.

**iOS (SWIFT)**

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.adBreakComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete) auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackEvent` mit dem `AdBreakComplete` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

## Mediensammlungs-API

Senden eines `adBreakComplete` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```
