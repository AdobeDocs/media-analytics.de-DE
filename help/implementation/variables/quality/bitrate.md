---
title: Bitrate
description: Legen Sie die aktuelle Wiedergabebitrate (in kbps) für das QoE-Objekt fest, damit das Backend Bitratenmetriken berechnen kann.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 6%

---


# Bitrate

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Bitrate**&#x200B;behandelt. Siehe [[!UICONTROL Durchschnittliche Bitrate] (Dimension)](/help/reporting/dimensions/average-bitrate.md) und [[!UICONTROL Durchschnittliche Bitrate] (Metrik)](/help/reporting/metrics/average-bitrate.md) für die entsprechenden Berichtsvariablen.*

>[!ENDSHADEBOX]

Die Bitratenvariable ist die aktuelle Wiedergabebitrate in Kilobit pro Sekunde. Legen Sie sie für das QoE-Objekt fest, wenn der Player eine Bitrate aushandelt, und aktualisieren Sie das QoE-Objekt, wenn sich die Bitrate ändert. Das Backend verwendet Bitratenwerte zur Berechnung [[!UICONTROL durchschnittlichen Bitrate]](/help/reporting/metrics/average-bitrate.md) der Dimension pro Bitraten-Bucket und der Metrik [[!UICONTROL Bitratenänderungen]](/help/reporting/metrics/bitrate-changes.md).

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.qoe.bitrateAverageBucket` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **Erforderlich** | Nein |
| **Gesendet mit** | Qualitätsereignisse ([Bitratenänderung](/help/implementation/events/playback/bitrate-change.md), [Pufferstart](/help/implementation/events/playback/buffer-start.md), [Fehler](/help/implementation/events/error.md)), Sitzungsschluss |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Legen Sie beim Aufrufen von [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) `bitrate` in `xdm.mediaCollection.qoeDataDetails` auf `media.bitrateChange` (oder ein qualitätsbezogenes Ereignis) fest:

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

Übergeben Sie die Bitrate als erstes Argument an `createQoEObject`. Aktualisieren Sie das QoE-Objekt im Tracker, bevor ein Qualitätsereignis ausgelöst wird.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Übergeben Sie die Bitrate als erstes Argument an `createQoEObject`. Aktualisieren Sie das QoE-Objekt im Tracker, bevor ein Qualitätsereignis ausgelöst wird.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

Legen Sie `bitrate` innerhalb von `xdm.mediaCollection.qoeDataDetails` fest, wenn Sie `sendMediaEvent` für Qualitätsereignisse wie `media.bitrateChange` aufrufen:

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

Rufen Sie den [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)-Endpunkt mit `bitrate` in `xdm.mediaCollection.qoeDataDetails` auf:

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Übergeben Sie die Bitrate in kbps als erstes Argument, um den Tracker zu `ADBMobile.media.createQoSObject` und zu aktualisieren:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
