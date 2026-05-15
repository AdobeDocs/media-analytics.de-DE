---
title: Bitrate
description: Legen Sie die aktuelle Wiedergabebitrate (in kbps) für das QoE-Objekt fest, damit das Backend Bitratenmetriken berechnen kann.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 10%

---


# Bitrate

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Bitrate**&#x200B;behandelt. Siehe [Durchschnittliche Bitrate (Dimension)](/help/reporting/dimensions/average-bitrate.md) und [Durchschnittliche Bitrate (Metrik)](/help/reporting/metrics/average-bitrate.md) für die entsprechenden Berichtsvariablen.*

>[!ENDSHADEBOX]

Die Bitratenvariable ist die aktuelle Wiedergabebitrate in Kilobit pro Sekunde. Legen Sie sie für das QoE-Objekt fest, wenn der Player eine Bitrate aushandelt, und aktualisieren Sie das QoE-Objekt, wenn sich die Bitrate ändert. Das Backend verwendet Bitratenwerte zur Berechnung der durchschnittlichen Bitrate, der Dimension pro Bitraten-Bucket und der Metrik „Bitratenänderungen“.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.qoe.bitrateAverageBucket` |
| **XDM-Sammlungsfeld** | [`mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **Erforderlich** | Nein |
| **Gesendet mit** | Qualitätsereignisse ([Bitratenänderung](/help/implementation/events/playback/bitrate-change.md), [Pufferstart](/help/implementation/events/playback/buffer-start.md), [Fehler](/help/implementation/events/error.md)), Sitzungsschluss |

## Web SDK

Legen Sie beim Aufrufen von [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) `bitrate` in `mediaCollection.qoeDataDetails` auf `media.bitrateChange` (oder ein qualitätsbezogenes Ereignis) fest:

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

## Mobile SDK

Übergeben Sie die Bitrate als erstes Argument an `createQoEObject`. Aktualisieren Sie das QoE-Objekt im Tracker, bevor ein Qualitätsereignis ausgelöst wird.

**iOS (SWIFT)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Legen Sie `bitrate` innerhalb von `mediaCollection.qoeDataDetails` fest, wenn Sie `sendMediaEvent` für Qualitätsereignisse wie `media.bitrateChange` aufrufen:

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

## Media Edge-API

Rufen Sie den [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)-Endpunkt mit `bitrate` in `mediaCollection.qoeDataDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die Bitrate als erstes Argument für die `ADB.Media.createQoEObject` und aktualisieren Sie den Tracker:

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

## Mediensammlungs-API

Fügen Sie `media.qoe.bitrate` in das `params` Ihrer `bitrateChange` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
