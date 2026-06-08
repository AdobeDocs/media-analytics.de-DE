---
title: Anzeigenposition im Pod
description: Legen Sie die Indexposition der Anzeige innerhalb der übergeordneten Anzeigenunterbrechung fest. Die erste Anzeige hat den Index 0.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# Anzeigenposition im Pod

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Anzeige in Pod-Position**behandelt. Siehe [Anzeige in Pod-Position](/help/reporting/dimensions/ad-in-pod-position.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Variable „Anzeige im Pod“ ist die nullindizierte Position der Anzeige innerhalb der übergeordneten Anzeigenunterbrechung. Die erste Anzeige in einem Pod hat einen Index `0`, die zweite einen Index `1` usw. Verwenden Sie die Dimension, um Interaktion und Abschluss nach Position innerhalb einer Werbeunterbrechung zu vergleichen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.ad.podPosition` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.ad.podPosition` |
| **Erforderlich** | Ja |
| **Gesendet mit** | [Anzeigenstart](/help/implementation/events/ads/ad-start.md), Anzeigenschluss |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`podPosition` in `xdm.mediaCollection.advertisingDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie die Position als drittes Argument an `createAdObject`.

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

Übergeben Sie die Position als drittes Argument an `createAdObject`.

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku Edge]

Legen Sie `podPosition` in `xdm.mediaCollection.advertisingDetails` fest, wenn Sie `sendMediaEvent` für `media.adStart` aufrufen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "podPosition": 0,
                "length": 15,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den Endpunkt [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) mit `podPosition` in `xdm.mediaCollection.advertisingDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
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

Übergeben Sie die Position als drittes Argument für `ADB.Media.createAdObject`:

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Übergeben Sie die Position als drittes Argument für `ADBMobile.media.createAdObject`:

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",
  "ad-2125",
  1,
  30
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Übergeben Sie die Position als drittes Argument an `adb_media_init_adinfo`. Die Anzeigenposition innerhalb des Pods ist 1-basiert:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB Media Collection API]

`media.ad.podPosition` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.podPosition": 0
  }
}
```

Die vollständige Anfragestruktur [ Sie in der ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]
