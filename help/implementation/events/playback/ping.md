---
title: Ping
description: Senden Sie einen Heartbeat, um die Mediensitzung am Leben zu erhalten und den Wiedergabegeschritt in regelmäßigen Abständen zu verfolgen.
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
source-wordcount: '292'
ht-degree: 1%
---

# Ping

Das Ping-Ereignis ist ein Heartbeat, der die Sitzung am Leben erhält und den Wiedergabegeschritt verfolgt. Senden Sie es während der gesamten Wiedergabe auf einem Timer. Bei Mobile SDKs werden Pings automatisch gesendet. Auf allen anderen Plattformen müssen sie im angegebenen Intervall manuell gesendet werden.

* **Hauptinhalt** zuerst Ping 10 Sekunden nach dem Wiedergabebeginn und danach alle 10 Sekunden
* **Anzeigeninhalt**: alle 1 Sekunde beim Anzeigen-Tracking

Fügen Sie kein `params` Objekt in den Textkörper der Ping-Anfrage ein.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: Keine

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Mobile SDK sendet automatisch Ping-Ereignisse. Es ist kein expliziter Aufruf erforderlich.

>[!TAB Android]

Mobile SDK sendet automatisch Ping-Ereignisse. Es ist kein expliziter Aufruf erforderlich.

>[!TAB Roku Edge]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK sendet automatisch Ping-Ereignisse. Es ist kein expliziter Aufruf erforderlich.

>[!TAB Chromecast]

Die Chromecast-SDK sendet automatisch Ping-Ereignisse. Es ist kein expliziter Aufruf erforderlich.

>[!TAB Roku 2.x]

Media SDK sendet automatisch Ping-Ereignisse, solange Sie `processMediaMessages` in Ihrer Ereignisschleife aufrufen. Aktualisieren Sie den Abspielkopf so, dass jeder Ping die aktuelle Position anzeigt:

```brightscript
ADBMobile().mediaUpdatePlayhead(10)
```

>[!TAB Media Collection API]

Senden Sie einen `ping` POST an den [events-Endpunkt](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) auf einem Timer. `params` Objekt nicht einschließen:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```

>[!ENDTABS]
