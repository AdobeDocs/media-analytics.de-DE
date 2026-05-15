---
title: Sitzung abgeschlossen
description: Signal, dass der Betrachter das Ende des Hauptinhalts erreicht hat.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 16%

---


# Sitzung abgeschlossen

Das Ereignis „Session Complete“ signalisiert, dass der Viewer das Ende des Hauptinhalts erreicht hat. Die Sitzung wird nicht sofort geschlossen. Die Sitzung bleibt geöffnet, bis sie von selbst abläuft. Wenn Sie die Sitzung sofort schließen möchten, rufen Sie stattdessen &quot;[&quot; ](session-end.md).

* **Voraussetzungen**: [Sitzungsstart](session-start.md)
* **Zugeordnete Metrik**: [Inhalt abgeschlossen](/help/reporting/metrics/content-completes.md)

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.sessionComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackComplete` auf, wenn der Medien-Player das Ende des Inhalts erreicht.

**iOS (SWIFT)**

```swift
tracker.trackComplete()
```

**Android (Kotlin)**

```kotlin
tracker.trackComplete()
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.sessionComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackComplete` auf, wenn der Medien-Player das Ende des Inhalts erreicht:

```javascript
tracker.trackComplete();
```

## Mediensammlungs-API

Senden Sie einen `sessionComplete` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```
