---
title: Fehler
description: Signal, dass der Medienplayer auf einen Fehler gestoßen ist.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 16%

---


# Fehler

Das Fehlerereignis signalisiert, dass der Media Player auf einen Fehler gestoßen ist. Beim Verfolgen eines Fehlers wird die Sitzung nicht geschlossen. Wenn der Fehler verhindert, dass die Wiedergabe fortgesetzt wird, rufen [&#x200B; nach dem &#x200B;](session/session-end.md) „Sitzungsende“ auf.

* **Voraussetzungen**: [Sitzungsstart](session/session-start.md)
* **Zugeordnete Metrik**: [Von Fehlern betroffene Streams](/help/reporting/metrics/error-impacted-streams.md)

Die `errorDetails.source`-Eigenschaft akzeptiert nur zwei Werte: `player` (Fehler, die vom Media-Player stammen) und `external` (Fehler von einer externen Quelle wie einem CDN oder Netzwerk).

## Web SDK

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.error"` und den erforderlichen `errorDetails` auf:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

`trackError` mit einer Fehler-ID-Zeichenfolge aufrufen.

**iOS (SWIFT)**

```swift
tracker.trackError(errorId: "media-error-001")
```

**Android (Kotlin)**

```kotlin
tracker.trackError("media-error-001")
```

## Roku (BrightScript)

Rufen Sie `sendMediaEvent` mit `eventType: "media.error"` und den erforderlichen `errorDetails` auf:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

## Media Edge-API

Rufen Sie den [error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/)-Endpunkt mit dem erforderlichen `errorDetails` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

`trackError` mit einer Fehler-ID-Zeichenfolge aufrufen:

```javascript
tracker.trackError("media-error-001");
```

## Mediensammlungs-API

Senden eines `error` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```
