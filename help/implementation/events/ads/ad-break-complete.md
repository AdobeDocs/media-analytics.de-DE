---
title: Werbeunterbrechung abgeschlossen
description: Signal, dass alle Anzeigen in einer Werbeunterbrechung beendet sind.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# Werbeunterbrechung abgeschlossen

Das Ereignis „Anzeigenunterbrechung abgeschlossen“ signalisiert, dass alle Anzeigen in einer Anzeigenunterbrechung abgeschlossen (entweder abgeschlossen oder übersprungen) sind. Dadurch wird die durch „Start der Werbeunterbrechung[&#x200B; geöffnete Werbeunterbrechung &#x200B;](ad-break-start.md).

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md), [Start der Werbeunterbrechung](ad-break-start.md)
* **Zugeordnete Metrik**: Keine

>[!IMPORTANT]
>
>Jeder `adBreakStart` muss einen passenden `adBreakComplete` haben. Ohne das schließende Bookend werden Anzeigenereignisse ignoriert und die Anzeigendauer wird dem Hauptinhalt zugeordnet.

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.adBreakComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Rufen Sie `trackEvent` mit dem `AdBreakComplete` Ereignistyp auf.

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Rufen Sie `trackEvent` mit dem `AdBreakComplete` Ereignistyp auf.

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku]

`sendMediaEvent` mit `eventType: "media.adBreakComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den Endpunkt [adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete) auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
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

Rufen Sie `trackEvent` mit dem `AdBreakComplete` Ereignistyp auf:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

Rufen Sie `trackEvent` mit dem `AdBreakComplete` Ereignistyp auf:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB Media Collection API]

Senden eines `adBreakComplete` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
