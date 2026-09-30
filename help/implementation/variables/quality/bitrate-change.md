---
title: Bitratenänderung
description: Lösen Sie ein Bitratenänderungsereignis aus, wenn der Player zu einer anderen Bitrate wechselt.
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
source-wordcount: '287'
ht-degree: 6%
---

# Bitratenänderung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird beschrieben, wie Sie Bitratenänderungsereignisse implementieren. Siehe [[!UICONTROL Bitratenänderungen] (Dimension)](/help/reporting/dimensions/bitrate-changes.md) und [[!UICONTROL Bitratenänderungen] (Metrik)](/help/reporting/metrics/bitrate-changes.md) für die entsprechenden Berichtsvariablen.*

>[!ENDSHADEBOX]

Das Bitratenänderungsereignis signalisiert, dass der Player zu einer anderen Bitrate gewechselt hat. Aktualisieren Sie zunächst den [Bitrate](/help/implementation/variables/quality/bitrate.md)-Wert für das QoE-Objekt und lösen Sie dann das Bitratenänderungsereignis aus. Das Backend verwendet die Anzahl dieser Ereignisse, um die Metrik [[!UICONTROL Bitratenänderungen]](/help/reporting/dimensions/bitrate-changes.md) und [[!UICONTROL Bitratenänderungen]](/help/reporting/metrics/bitrate-changes.md) und den resultierenden Bitratenwert-Feed [[!UICONTROL durchschnittliche Bitrate]](/help/reporting/metrics/average-bitrate.md) zu berechnen.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | (keine — vom Backend gezählt) |
| **XDM-Ereignistyp** | `media.bitrateChange` |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Bitratenänderung](/help/implementation/events/playback/bitrate-change.md) |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Aktualisieren Sie das QoE-Objekt mit der neuen Bitrate und lösen Sie dann das Bitratenänderungsereignis aus.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Aktualisieren Sie das QoE-Objekt mit der neuen Bitrate und lösen Sie dann das Bitratenänderungsereignis aus.

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB Media Edge-API]

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

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Aktualisieren Sie das QoE-Objekt und lösen Sie das Ereignis aus:

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

Aktualisieren Sie das QoS-Objekt mit der neuen Bitrate und lösen Sie dann das Bitratenänderungsereignis aus:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  4500,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

Aktualisieren Sie das QoS-Objekt mit der neuen Bitrate und lösen Sie dann das Bitratenänderungsereignis aus:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(4500.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB Media Collection API]

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

Die vollständige Anfragestruktur [ Sie in der ](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]
