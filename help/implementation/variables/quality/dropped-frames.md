---
title: Abgelegte Frames
description: Legen Sie die Anzahl der Dropped Frames im QoE-Objekt fest, damit das Backend die Frame-Drop-Qualität melden kann.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 5%

---


# Abgelegte Frames

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Dropped Frames**behandelt. Siehe [Abgelegte Frames](/help/reporting/dimensions/dropped-frames.md) für die entsprechende Reporting-Dimension und -Metrik.*

>[!ENDSHADEBOX]

Die Variable Abgelegte Frames ist die laufende Anzahl an Frames, die der Player während der Sitzung abgelegt hat. Legen Sie ihn auf das QoE-Objekt fest und aktualisieren Sie den Wert, wenn der Player neue Abbrüche meldet. Das Backend meldet den neuesten Wert zum Sitzungsende.

>[!NOTE]
>
>Übergeben Sie immer die **kumulative Summe** der ausgelassenen Frames für die gesamte Sitzung bis zu diesem Punkt, nicht pro Intervall-Delta. Wenn Sie den Wert zwischen Aktualisierungen auf `0` zurücksetzen, erhält das Backend `0` als endgültigen Wert und meldet null abgelegte Frames für die Sitzung, unabhängig davon, was zuvor tatsächlich abgelegt wurde.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.qoe.droppedFrameCount` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **Erforderlich** | Nein |
| **Gesendet mit** | Qualitätsereignisse ([Bitratenänderung](/help/implementation/events/playback/bitrate-change.md), [Pufferstart](/help/implementation/events/playback/buffer-start.md), [Fehler](/help/implementation/events/error.md)), Sitzungsschluss |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

`droppedFrames` in `xdm.mediaCollection.qoeDataDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie abgelegte Frames als viertes Argument an `createQoEObject`. Aktualisieren Sie den Tracker, bevor ein Qualitätsereignis ausgelöst wird.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Übergeben Sie abgelegte Frames als viertes Argument an `createQoEObject`. Aktualisieren Sie den Tracker, bevor ein Qualitätsereignis ausgelöst wird.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

`droppedFrames` in `xdm.mediaCollection.qoeDataDetails` festlegen, wenn `sendMediaEvent` aufgerufen wird:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)-Endpunkt mit `droppedFrames` in `xdm.mediaCollection.qoeDataDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
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

Übergeben Sie abgelegte Frames als viertes Argument an `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Übergeben Sie die kumulative Dropped-Frame-Anzahl als viertes Argument, um den Tracker zu `ADBMobile.media.createQoSObject` und zu aktualisieren:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames (cumulative total)
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Übergeben Sie die kumulative Dropped-Frame-Anzahl als viertes Argument (`droppedFrames`), um den Tracker zu `adb_media_init_qosinfo` und mit `mediaUpdateQoS` zu aktualisieren:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB Media Collection API]

`media.qoe.droppedFrames` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

Die vollständige Anfragestruktur [ Sie in der ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .

>[!ENDTABS]
