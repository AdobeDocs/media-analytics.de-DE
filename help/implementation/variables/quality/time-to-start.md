---
title: Zeit bis zum Start
description: Legen Sie die Startzeit des Players in Millisekunden fest, damit das Backend die Zeit bis zum ersten Bild melden kann.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 6%

---


# Zeit bis zum Start

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **Time to Start**behandelt. Siehe [[!UICONTROL Zeit bis zum Start]](/help/reporting/dimensions/time-to-start.md) für die entsprechende Reporting-Dimension und -Metrik.*

>[!ENDSHADEBOX]

Die Variable time to start gibt die Zeit in Millisekunden an, die zwischen dem Player, der die Wiedergabe startet, und dem ersten Frame-Rendering verstrichen ist. Legen Sie sie für das QoE-Objekt fest, bevor das Sitzungsstartereignis ausgelöst wird. Adobe speichert und meldet den Wert in Sekunden. Die Millisekunden vergehen und Adobe konvertiert bei der Aufnahme.

>[!IMPORTANT]
>
>Sobald der Player mit dem Rendern von Inhaltsrahmen beginnt, beenden Sie die Aktualisierung von `timeToStart`. Der Wert kann während der anfänglichen Puffer- oder Ladephase ansteigen, sollte jedoch ab dem Zeitpunkt, zu dem die Wiedergabe beginnt, als festgelegt behandelt werden. Wenn Sie die Metrik nach dem Rendern des ersten Frames weiterhin aktualisieren, wird eine überhöhte oder falsche [[!UICONTROL Time to Start]](/help/reporting/metrics/time-to-start.md) erzeugt.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.qoe.timeToStart` |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager-Eigenschaft** | `c_contextdata.a.media.qoe.timeToStart` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md), Sitzung schließen |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Legen Sie beim Aufrufen von [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) `timeToStart` in `xdm.mediaCollection.qoeDataDetails` auf `media.sessionStart` fest:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Übergeben Sie die Startzeit als zweites Argument (`startupTime`) an `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Übergeben Sie die Startzeit als zweites Argument (`startupTime`) an `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

Legen Sie beim Aufrufen von `createMediaSession` `timeToStart` in `xdm.mediaCollection.qoeDataDetails` auf `media.sessionStart` fest:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `timeToStart` in `xdm.mediaCollection.qoeDataDetails` auf:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Übergeben Sie die Zeit für den Start als zweites zu `ADB.Media.createQoEObject` Argument:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Übergeben Sie die Startzeit in Millisekunden als zweites Argument (`startupTime`), um den Tracker zu `ADBMobile.media.createQoSObject` und zu aktualisieren:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,   // bitrate
  0,      // startupTime (ms)
  24,     // fps
  0       // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Media Collection API]

`media.qoe.timeToStart` in das `params` Objekt in `sessionStart` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
