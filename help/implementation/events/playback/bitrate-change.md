---
title: Bitratenänderung
description: Signal zur Änderung der Wiedergabebitrate.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# Bitratenänderung

Das Bitratenänderungsereignis signalisiert, dass der Player eine neue Wiedergabebitrate ausgehandelt hat. Wird gesendet, wenn sich die Bitrate während der Wiedergabe ändert. Schließen Sie den neuen Bitratenwert in die QoE-Daten ein, damit das Backend [[!UICONTROL durchschnittliche Bitrate]](/help/reporting/metrics/average-bitrate.md) und die Dimension pro Bitraten-Bucket berechnen kann.

* **Voraussetzungen**: [Sitzungsstart](../session/session-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Bitratenänderungen]](/help/reporting/metrics/bitrate-changes.md)

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.bitrateChange"` und der neuen Bitrate in `qoeDataDetails`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Erstellen Sie ein QoE-Objekt mit der neuen Bitrate und aktualisieren Sie den Tracker, bevor das Bitratenänderungsereignis ausgelöst wird.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Erstellen Sie ein QoE-Objekt mit der neuen Bitrate und aktualisieren Sie den Tracker, bevor das Bitratenänderungsereignis ausgelöst wird.

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku]

`sendMediaEvent` mit `eventType: "media.bitrateChange"` und der neuen Bitrate in `qoeDataDetails`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/)-Endpunkt mit der neuen Bitrate in `qoeDataDetails` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
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

Erstellen Sie ein QoE-Objekt mit der neuen Bitrate und aktualisieren Sie den Tracker:

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

Aktualisieren Sie das vom `getQoSObject`-Delegaten zurückgegebene QoS-Objekt und verfolgen Sie dann das Ereignis:

```javascript
// Update QoS data via the delegate
this._qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // dropped frames
  24,    // fps
  0      // startup time
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Media Collection API]

Senden Sie eine `bitrateChange`-POST-Anfrage an [events-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) mit der neuen Bitrate in `qoeData`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```

>[!ENDTABS]
