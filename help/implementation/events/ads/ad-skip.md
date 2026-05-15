---
title: Überspringen einer Anzeige
description: Signal, dass der Betrachter eine Anzeige übersprungen hat.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---


# Überspringen einer Anzeige

Das Ereignis zum Überspringen einer Anzeige signalisiert, dass der Viewer eine Anzeige übersprungen hat, bevor sie beendet wurde. Senden, wenn der Viewer auf die Schaltfläche Überspringen klickt. Senden Sie [Anzeige abgeschlossen](ad-complete.md) anstelle der Anzeige, die bis zum Abschluss abgespielt wird.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Anzeigenunterbrechungsstart](ad-break-start.md), [Anzeigenstart](ad-start.md)
* **Zugeordnete Metrik**: Keine

>[!IMPORTANT]
>
>Dieses Ereignis muss von `adBreakStart` und `adBreakComplete` Buchstützen umgeben sein, selbst wenn eine einzige Anzeige abgespielt wird. Ohne diese Buchstützen werden Anzeigenereignisse ignoriert und die Anzeigendauer wird als Hauptinhaltsdauer gezählt.

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.adSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackEvent` mit dem `AdSkip` Ereignistyp auf.

**iOS (SWIFT)**

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.adSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip) auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackEvent` mit dem `AdSkip` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

## Mediensammlungs-API

Senden eines `adSkip` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```
