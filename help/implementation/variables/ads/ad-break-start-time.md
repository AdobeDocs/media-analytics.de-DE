---
title: Startzeit der Werbeunterbrechung
description: Legen Sie die Startzeit (Offset) der Anzeigenunterbrechung innerhalb des Inhalts in Sekunden fest.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 12%

---


# Startzeit der Werbeunterbrechung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Startzeit der Werbeunterbrechung**&#x200B;behandelt. Siehe [Pod-Position](/help/reporting/dimensions/pod-position.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Startzeitvariable für die Anzeigenunterbrechung ist der Versatz der Anzeigenunterbrechung innerhalb des Inhalts, gemessen in Sekunden. Bei einem Pre-Roll ist der Wert `0`; bei einem Mid-Roll ist der Wert die Abspielposition, an der die Pause beginnt.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.podSecond` |
| **XDM-Sammlungsfeld** | [`mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Erforderlich** | Ja |
| **Gesendet mit** | Anzeigenstart, Anzeigenschluss |

## Web SDK

`offset` in `mediaCollection.advertisingPodDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Übergeben Sie die Startzeit in Sekunden als drittes Argument an `createAdBreakObject`.

**iOS (SWIFT)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Legen Sie `offset` in `mediaCollection.advertisingPodDetails` fest, wenn Sie `sendMediaEvent` für `media.adBreakStart` aufrufen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

## Media Edge-API

Rufen Sie den Endpunkt [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) mit `offset` in `mediaCollection.advertisingPodDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Startzeit als drittes Argument für `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Mediensammlungs-API

Fügen Sie `media.ad.podSecond` in das `params` Ihrer `adBreakStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
