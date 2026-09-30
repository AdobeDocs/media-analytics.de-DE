---
title: Frames pro Sekunde
description: Legen Sie die aktuelle Framerate für das QoE-Objekt so fest, dass das Backend über einen Framerate-Kontext für Qualitätsberichte verfügt.
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
source-wordcount: '281'
ht-degree: 7%
---

# Frames pro Sekunde

Die Variable „Frames pro Sekunde“ ist die aktuelle Framerate des Streams. Legen Sie sie auf dem QoE-Objekt neben Bitrate und Dropped Frames fest, damit das Backend für jede Wiedergabesitzung Kontext in voller Qualität hat. Adobe Analytics erstellt nicht automatisch eine Berichtsvariable für die Framerate. Erstellen Sie eine benutzerdefinierte Verarbeitungsregel, wenn sie als Bericht angezeigt werden soll.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | Keine (Adobe Analytics weist keinen reservierten Kontextdatenschlüssel für die Framerate zu) |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager-Eigenschaft** | nicht angegeben |
| **Erforderlich** | Nein |
| **Gesendet mit** | Qualitätsereignisse ([Bitratenänderung](/help/implementation/events/playback/bitrate-change.md), [Pufferstart](/help/implementation/events/playback/buffer-start.md), [Fehler](/help/implementation/events/error.md)), Sitzungsschluss |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`framesPerSecond` in `xdm.mediaCollection.qoeDataDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie die Framerate als drittes Argument (`fps`) an `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Übergeben Sie die Framerate als drittes Argument (`fps`) an `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

`framesPerSecond` in `xdm.mediaCollection.qoeDataDetails` festlegen, wenn `sendMediaEvent` aufgerufen wird:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)-Endpunkt mit `framesPerSecond` in `xdm.mediaCollection.qoeDataDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
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

Übergeben Sie die Framerate als drittes Argument für `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Übergeben Sie die Framerate als drittes Argument (`fps`), um den Tracker zu `ADBMobile.media.createQoSObject` und zu aktualisieren:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Übergeben Sie die Framerate als drittes Argument (`fps`), um den Tracker mit `mediaUpdateQoS` zu `adb_media_init_qosinfo` und zu aktualisieren:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB Media Collection API]

`media.qoe.framesPerSecond` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

Die vollständige Anfragestruktur [ Sie in der ](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]
