---
title: Kapitelübersprung
description: Signal, dass der Betrachter ein Kapitel übersprungen hat.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 18%

---


# Kapitelübersprung

Das Ereignis „Kapitelüberspringen“ signalisiert, dass der Viewer ein Kapitel übersprungen hat, bevor es beendet wurde. Senden Sie ihn, wenn der Betrachter über die Kapitelgrenze hinweg navigiert, ohne ihn bis zum Abschluss zu beobachten. Senden Sie [Kapitel abgeschlossen](chapter-complete.md) wenn das Kapitel bis zu seinem Ende abgespielt wird.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Kapitelstart](chapter-start.md)
* **Zugeordnete Metrik**: Keine

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.chapterSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackEvent` mit dem `ChapterSkip` Ereignistyp auf.

**iOS (SWIFT)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.chapterSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

## Media Edge-API

Rufen Sie den [chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackEvent` mit dem `ChapterSkip` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

## Mediensammlungs-API

Senden Sie einen `chapterSkip` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```
