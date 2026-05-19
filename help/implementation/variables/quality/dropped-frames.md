---
title: Abgelegte Frames
description: Legen Sie die Anzahl der Dropped Frames im QoE-Objekt fest, damit das Backend die Frame-Drop-Qualität melden kann.
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 9%

---


# Abgelegte Frames

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Dropped Frames**&#x200B;behandelt. Siehe [Abgelegte Frames](/help/reporting/dimensions/dropped-frames.md) für die entsprechende Reporting-Dimension und -Metrik.*

>[!ENDSHADEBOX]

Die Variable Abgelegte Frames ist die laufende Anzahl an Frames, die der Player während der Sitzung abgelegt hat. Legen Sie ihn auf das QoE-Objekt fest und aktualisieren Sie den Wert, wenn der Player neue Abbrüche meldet. Das Backend meldet den neuesten Wert zum Sitzungsende.

>[!NOTE]
>
>Übergeben Sie immer die **kumulative Summe** der ausgelassenen Frames für die gesamte Sitzung bis zu diesem Punkt, nicht pro Intervall-Delta. Wenn Sie den Wert zwischen Aktualisierungen auf `0` zurücksetzen, erhält das Backend `0` als endgültigen Wert und meldet null abgelegte Frames für die Sitzung, unabhängig davon, was zuvor tatsächlich abgelegt wurde.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.qoe.droppedFrameCount` |
| **XDM-Sammlungsfeld** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **Erforderlich** | Nein |
| **Gesendet mit** | Qualitätsereignisse ([Bitratenänderung](/help/implementation/events/playback/bitrate-change.md), [Pufferstart](/help/implementation/events/playback/buffer-start.md), [Fehler](/help/implementation/events/error.md)), Sitzungsschluss |

## Web SDK

`droppedFrames` in `mediaCollection.qoeDataDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

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

## Mobile SDK

Übergeben Sie abgelegte Frames als viertes Argument an `createQoEObject`. Aktualisieren Sie den Tracker, bevor ein Qualitätsereignis ausgelöst wird.

**iOS (SWIFT)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

`droppedFrames` in `mediaCollection.qoeDataDetails` festlegen, wenn `sendMediaEvent` aufgerufen wird:

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

## Media Edge-API

Rufen Sie den [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)-Endpunkt mit `droppedFrames` in `mediaCollection.qoeDataDetails` auf:

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

## Medien-SDK

Übergeben Sie abgelegte Frames als viertes Argument an `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## Mediensammlungs-API

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

Die vollständige Anfragestruktur [&#x200B; Sie in der &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) zur Mediensammlungs-API-Ereignisreferenz .
