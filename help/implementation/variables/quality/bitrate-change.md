---
title: Bitratenänderung
description: Lösen Sie ein Bitratenänderungsereignis aus, wenn der Player zu einer anderen Bitrate wechselt.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 11%

---


# Bitratenänderung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird beschrieben, wie Sie Bitratenänderungsereignisse implementieren. Siehe [Bitratenänderungen (Dimension)](/help/reporting/dimensions/bitrate-changes.md) und [Bitratenänderungen (Metrik)](/help/reporting/metrics/bitrate-changes.md) für die entsprechenden Berichtsvariablen.*

>[!ENDSHADEBOX]

Das Bitratenänderungsereignis signalisiert, dass der Player zu einer anderen Bitrate gewechselt hat. Aktualisieren Sie zunächst den [Bitrate](/help/implementation/variables/quality/bitrate.md)-Wert für das QoE-Objekt und lösen Sie dann das Bitratenänderungsereignis aus. Das Backend verwendet die Anzahl dieser Ereignisse, um die Dimensionsänderungen und Metrik der Bitrate zu berechnen, und die resultierenden Bitratenwerte liefern die durchschnittliche Bitrate.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | (keine — vom Backend gezählt) |
| **XDM-Ereignistyp** | `media.bitrateChange` |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Bitratenänderung](/help/implementation/events/playback/bitrate-change.md) |

## Web SDK

Verwenden Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) , um ein `media.bitrateChange`-Ereignis mit der neuen Bitrate zu senden:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## Mobile SDK

Aktualisieren Sie das QoE-Objekt mit der neuen Bitrate und lösen Sie dann das Bitratenänderungsereignis aus.

**iOS (SWIFT)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

Verwenden Sie `sendMediaEvent` mit `media.bitrateChange`, um eine Bitratenänderung zu signalisieren. Neue Bitrate in `qoeDataDetails` einschließen:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## Media Edge-API

Rufen Sie den [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)-Endpunkt mit dem aktualisierten `qoeDataDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## Medien-SDK

Aktualisieren Sie das QoE-Objekt und lösen Sie das Ereignis aus:

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## Mediensammlungs-API

Senden Sie eine `bitrateChange` POST-Anfrage mit der neuen Bitrate:

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

Die vollständige Anfragestruktur [ Sie in der ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
