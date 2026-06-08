---
title: Start anhalten
description: Signal, dass die Medienwiedergabe angehalten wurde.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# Start anhalten

Das Pause-Start-Ereignis signalisiert, dass der Benutzer die Wiedergabe angehalten hat. Es gibt kein separates Fortsetzungsereignis. Senden Sie ein [Play](play.md)-Ereignis, wenn die Wiedergabe fortgesetzt wird.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Ereignisse anhalten]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>Es gibt keinen Resume-Ereignistyp. Eine Wiederaufnahme wird abgeleitet, wenn Sie nach der `pauseStart` ein [`play`](play.md) Ereignis senden.

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.pauseStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

>[!TAB iOS]

Ruft `trackPause` auf, wenn der Benutzer die Wiedergabe pausiert.

```swift
tracker.trackPause()
```

>[!TAB Android]

Ruft `trackPause` auf, wenn der Benutzer die Wiedergabe pausiert.

```kotlin
tracker.trackPause()
```

>[!TAB Roku Edge]

`sendMediaEvent` mit `eventType: "media.pauseStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
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

`trackPause` aufrufen, wenn der Benutzer die Wiedergabe pausiert:

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

`trackPause` aufrufen, wenn der Benutzer die Wiedergabe pausiert:

```javascript
ADBMobile.media.trackPause();
```

>[!TAB Roku 2.x]

`mediaTrackPause` aufrufen, wenn der Benutzer die Wiedergabe pausiert:

```brightscript
ADBMobile().mediaTrackPause()
```

>[!TAB Media Collection API]

Senden Sie einen `pauseStart` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
