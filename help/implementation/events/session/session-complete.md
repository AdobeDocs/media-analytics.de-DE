---
title: Sitzung abgeschlossen
description: Signal, dass der Betrachter das Ende des Hauptinhalts erreicht hat.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%
---

# Sitzung abgeschlossen

Das Ereignis „Session Complete“ signalisiert, dass der Viewer das Ende des Hauptinhalts erreicht hat. Die Sitzung wird nicht sofort geschlossen. Die Sitzung bleibt geöffnet, bis sie von selbst abläuft. Wenn Sie die Sitzung sofort schließen möchten, rufen Sie stattdessen &quot;[&quot; &#x200B;](session-end.md).

* **Voraussetzungen**: [Sitzungsstart](session-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Inhalt abgeschlossen]](/help/reporting/metrics/content-completes.md)

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.sessionComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

>[!TAB iOS]

Rufen Sie `trackComplete` auf, wenn der Medien-Player das Ende des Inhalts erreicht.

```swift
tracker.trackComplete()
```

>[!TAB Android]

Rufen Sie `trackComplete` auf, wenn der Medien-Player das Ende des Inhalts erreicht.

```kotlin
tracker.trackComplete()
```

>[!TAB Roku Edge]

`sendMediaEvent` mit `eventType: "media.sessionComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
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

Rufen Sie `trackComplete` auf, wenn der Medien-Player das Ende des Inhalts erreicht:

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

Rufen Sie `trackComplete` auf, wenn der Medien-Player das Ende des Inhalts erreicht:

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

Rufen Sie `mediaTrackComplete` auf, wenn der Medien-Player das Ende des Inhalts erreicht:

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB Media Collection API]

Senden Sie einen `sessionComplete` POST an den [events-Endpunkt](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
