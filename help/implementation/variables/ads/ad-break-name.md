---
title: Name der Werbeunterbrechung
description: Legen Sie den Anzeigenamen der übergeordneten Anzeigenunterbrechung fest.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 12%

---


# Name der Werbeunterbrechung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Anzeigenumbruch-Name**&#x200B;behandelt. Siehe [Pod-Name](/help/reporting/dimensions/pod-name.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable Name der Werbeunterbrechung ist der Anzeigename der Werbeunterbrechung (z. B. `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). Der Wert wird für das Objekt der Anzeigenunterbrechung festgelegt, nicht für einzelne Anzeigen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.podFriendlyName` |
| **XDM-Sammlungsfeld** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Erforderlich** | Ja (Mobile SDK); Nein (Edge, Mediensammlungs-API) |
| **Gesendet mit** | Anzeigenstart, Anzeigenschluss |

## Web SDK

Legen Sie `friendlyName` in `mediaCollection.advertisingPodDetails` fest, wenn Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) für `media.adBreakStart` aufrufen:

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

Übergeben Sie den Namen der Anzeigenunterbrechung als erstes (`name`) Argument an `createAdBreakObject` und verfolgen Sie dann das Ereignis „ad-break-start“ vor dem Ereignis „ad-start“.

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
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Legen Sie `friendlyName` in `mediaCollection.advertisingPodDetails` fest, wenn Sie `sendMediaEvent` für `media.adBreakStart` aufrufen:

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

Rufen Sie den Endpunkt [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) mit `friendlyName` in `mediaCollection.advertisingPodDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie den Namen der Werbeunterbrechung als erstes Argument für `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Mediensammlungs-API

Fügen Sie `media.ad.podFriendlyName` in das `params` Ihrer `adBreakStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
