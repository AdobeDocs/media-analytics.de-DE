---
title: Name der Werbeunterbrechung
description: Legen Sie den Anzeigenamen der übergeordneten Anzeigenunterbrechung fest.
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
source-wordcount: '276'
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

>[!TAB Roku Edge]

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

>[!TAB Roku 2.x]

Übergeben Sie den Namen der Werbeunterbrechung als erstes Argument an `adb_media_init_adbreakinfo`. Beachten Sie die Roku-Parameter-Reihenfolge: `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("pre-roll", 0.0, 1)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
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

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]
