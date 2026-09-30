---
title: Hinzufügen abgeschlossen
description: Signal, dass die Wiedergabe einer einzelnen Anzeige abgeschlossen ist.
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
source-wordcount: '182'
ht-degree: 8%
---

# Hinzufügen abgeschlossen

Das Ereignis „Anzeige abgeschlossen“ signalisiert, dass die Wiedergabe einer einzelnen Anzeige abgeschlossen ist. Senden Sie es, nachdem die Anzeige bis zum Ende abgespielt wurde. Wenn der Viewer die Anzeige überspringt, senden Sie stattdessen [Anzeige überspringen](ad-skip.md).

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Anzeigenunterbrechungsstart](ad-break-start.md), [Anzeigenstart](ad-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Anzeige abgeschlossen]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Dieses Ereignis muss von `adBreakStart` und `adBreakComplete` Buchstützen umgeben sein, selbst wenn eine einzige Anzeige abgespielt wird. Ohne diese Buchstützen werden Anzeigenereignisse ignoriert und die Anzeigendauer wird als Hauptinhaltsdauer gezählt.

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.adComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

>[!TAB iOS]

Rufen Sie `trackEvent` mit dem `AdComplete` Ereignistyp auf.

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Rufen Sie `trackEvent` mit dem `AdComplete` Ereignistyp auf.

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku Edge]

`sendMediaEvent` mit `eventType: "media.adComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den Endpunkt [adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete) auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
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

Rufen Sie `trackEvent` mit dem `AdComplete` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

Rufen Sie `trackEvent` mit dem `AdComplete` Ereignistyp auf:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB Roku 2.x]

Rufen Sie `mediaTrackEvent` mit dem `MEDIA_AD_COMPLETE` Ereignistyp auf:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_COMPLETE)
```

>[!TAB Media Collection API]

Senden eines `adComplete` POST an den [events-Endpunkt](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
