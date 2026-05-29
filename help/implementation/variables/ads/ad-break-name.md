---
title: Name der Werbeunterbrechung
description: Legen Sie den Anzeigenamen der übergeordneten Anzeigenunterbrechung fest.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 6%

---


# Name der Werbeunterbrechung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Anzeigenumbruch-Name**&#x200B;behandelt. Siehe [Pod-Name](/help/reporting/dimensions/pod-name.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable Name der Werbeunterbrechung ist der Anzeigename der Werbeunterbrechung (z. B. `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). Der Wert wird für das Objekt der Anzeigenunterbrechung festgelegt, nicht für einzelne Anzeigen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.podFriendlyName` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.ad.podFriendlyName` |
| **Erforderlich** | Ja (Mobile SDK); Nein (Edge, Mediensammlungs-API) |
| **Gesendet mit** | [Start der Werbeunterbrechung](/help/implementation/events/ads/ad-break-start.md) und Schließen der Anzeige |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Legen Sie `friendlyName` in `xdm.mediaCollection.advertisingPodDetails` fest, wenn Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) für `media.adBreakStart` aufrufen:

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

>[!TAB iOS]

Übergeben Sie den Namen der Anzeigenunterbrechung als erstes (`name`) Argument an `createAdBreakObject` und verfolgen Sie dann das Ereignis „ad-break-start“ vor dem Ereignis „ad-start“.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie den Namen der Anzeigenunterbrechung als erstes (`name`) Argument an `createAdBreakObject` und verfolgen Sie dann das Ereignis „ad-break-start“ vor dem Ereignis „ad-start“.

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku]

Legen Sie `friendlyName` in `xdm.mediaCollection.advertisingPodDetails` fest, wenn Sie `sendMediaEvent` für `media.adBreakStart` aufrufen:

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

>[!TAB Media Edge-API]

Rufen Sie den Endpunkt [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) mit `friendlyName` in `xdm.mediaCollection.advertisingPodDetails` auf:

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Übergeben Sie den Namen der Werbeunterbrechung als erstes Argument für `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

Übergeben Sie den Namen der Werbeunterbrechung als erstes Argument für `ADBMobile.media.createAdBreakObject`:

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",
  1,
  0
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
