---
title: Ping
description: Senden Sie einen Heartbeat, um die Mediensitzung am Leben zu erhalten und den Wiedergabegeschritt in regelmäßigen Abständen zu verfolgen.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Ping

Das Ping-Ereignis ist ein Heartbeat, der die Sitzung am Leben erhält und den Wiedergabegeschritt verfolgt. Senden Sie es während der gesamten Wiedergabe auf einem Timer.

* **Hauptinhalt** zuerst Ping 10 Sekunden nach dem Wiedergabebeginn und danach alle 10 Sekunden
* **Anzeigeninhalt**: alle 1 Sekunde beim Anzeigen-Tracking

Fügen Sie kein `params` Objekt in den Textkörper der Ping-Anfrage ein.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: Keine

## Web SDK

Planen Sie einen wiederkehrenden `sendEvent` mit `eventType: "media.ping"`. Aktualisieren Sie bei jedem Aufruf `playhead` auf die aktuelle Wiedergabeposition:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

## Mobile SDK

Mobile SDK sendet automatisch Ping-Ereignisse. Es ist kein expliziter Aufruf erforderlich.

## Roku (BrightScript)

Planen Sie einen wiederkehrenden `sendMediaEvent` mit `eventType: "media.ping"`. Aktualisieren Sie bei jedem Aufruf `playhead` auf die aktuelle Wiedergabeposition:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

## Media Edge-API

Rufen Sie den [ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/)-Endpunkt in einem Timer auf. Adobe empfiehlt das erste Ping 10 Sekunden nach dem Beginn der Hauptwiedergabe, danach alle 10 Sekunden und danach alle 1 Sekunde während des Anzeigen-Trackings:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Media SDK sendet automatisch Ping-Ereignisse. Es ist kein expliziter Aufruf erforderlich.

## Mediensammlungs-API

Senden Sie einen `ping` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) auf einem Timer. `params` Objekt nicht einschließen:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```
