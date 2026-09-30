---
title: Kapitelübersprung
description: Signal, dass der Betrachter ein Kapitel übersprungen hat.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 9%
---

# Kapitelübersprung

Das Ereignis „Kapitelüberspringen“ signalisiert, dass der Viewer ein Kapitel übersprungen hat, bevor es beendet wurde. Senden Sie ihn, wenn der Betrachter über die Kapitelgrenze hinweg navigiert, ohne ihn bis zum Abschluss zu beobachten. Senden Sie [Kapitel abgeschlossen](chapter-complete.md) wenn das Kapitel bis zu seinem Ende abgespielt wird.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Kapitelstart](chapter-start.md)
* **Zugeordnete Metrik**: Keine

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Rufen Sie `trackEvent` mit dem `ChapterSkip` Ereignistyp auf.

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Rufen Sie `trackEvent` mit dem `ChapterSkip` Ereignistyp auf.

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Rufen Sie `trackEvent` mit dem `ChapterSkip` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

>[!TAB Chromecast]

Rufen Sie `trackEvent` mit dem `ChapterSkip` Ereignistyp auf:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
```

>[!TAB Roku 2.x]

Rufen Sie `mediaTrackEvent` mit dem `MEDIA_CHAPTER_SKIP` Ereignistyp auf:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_SKIP)
```

>[!TAB Media Collection API]

Senden Sie einen `chapterSkip` POST an den [events-Endpunkt](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```

>[!ENDTABS]
