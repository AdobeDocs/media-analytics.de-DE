---
title: Sitzungsende
description: Sofortiges Schließen einer Mediensitzung, wenn der Viewer Inhalte abbricht.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# Sitzungsende

Das Sitzungsende-Ereignis schließt eine Medienverfolgungssitzung sofort. Verwenden Sie sie, wenn der Viewer Inhalte abbricht, bevor das Ende erreicht ist, und Sie nicht möchten, dass nachfolgende Ereignisse unter derselben Sitzung verfolgt werden. Wenn der Viewer den Inhalt fertig gestellt hat, rufen Sie stattdessen [Sitzung abgeschlossen](session-complete.md) auf.

Ohne explizites Sitzungsende wird eine Sitzung automatisch nach 10 Minuten ohne Ereignisse oder 30 Minuten ohne Abspielkopfbewegung geschlossen.

* **Voraussetzungen**: [Sitzungsstart](session-start.md)
* **Zugeordnete Metrik**: Keine

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.sessionEnd"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

Rufen Sie `trackSessionEnd` auf, wenn der Viewer den Player schließt oder wegnavigiert.

**iOS (SWIFT)**

```swift
tracker.trackSessionEnd()
```

**Android (Kotlin)**

```kotlin
tracker.trackSessionEnd()
```

## Roku (BrightScript)

`sendMediaEvent` mit `eventType: "media.sessionEnd"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend)-Endpunkt auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Medien-SDK

Rufen Sie `trackSessionEnd` auf, wenn der Viewer den Player schließt oder wegnavigiert:

```javascript
tracker.trackSessionEnd();
```

## Mediensammlungs-API

Senden Sie einen `sessionEnd` POST an den [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
