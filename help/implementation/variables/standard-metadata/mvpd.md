---
title: MVPD
description: Legen Sie den Multichannel Video Programming Distributor fest, wenn sich der Anwender über Adobe Pass authentifiziert.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 15%

---


# MVPD

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **MVPD**&#x200B;behandelt. Siehe [MVPD](/help/reporting/dimensions/mvpd.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die MVPD-Variable (Multi-Channel Video Programming Distributor) ist der Kabel-, Satelliten- oder Virtual-MVPD-Provider, über den sich der Benutzer authentifiziert hat (z. B. `"Comcast"`, `"DirecTV"` oder `"YouTubeTV"`). Legen Sie sie fest, wenn Inhalte hinter der Adobe Pass- oder TV-Everywhere-Authentifizierung erfasst werden. Koppeln Sie mit [Autorisiert](/help/implementation/variables/standard-metadata/authorized.md), um zu verfolgen, welche Sitzungen die Authentifizierung abgeschlossen haben.

| Eigenschaft | Wert |
| --- | --- |
| **Kontextdatenvariable** | `a.media.pass.mvpd` |
| **XDM-Sammlungsfeld** | [`mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Erforderlich** | Nein |
| **Gesendet mit** | Sitzungsbeginn, Sitzungsabschluss |

## Web SDK

`mvpd` in `mediaCollection.sessionDetails` festlegen, wenn [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) aufgerufen wird:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Übergeben Sie die MVPD als Metadatenschlüssel im HashMap-Argument an `trackSessionStart`. Verwenden Sie `MediaConstants.VideoMetadataKeys.MVPD`.

**iOS (SWIFT)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Verwenden Sie `createMediaSession`, um `mvpd` in `sessionDetails` festzulegen:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge-API

Rufen Sie den [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)-Endpunkt mit `mvpd` in `mediaCollection.sessionDetails` auf:

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
          "channel": "Sports",
          "mvpd": "Comcast"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Medien-SDK

Übergeben Sie die MVPD im `contextData`-Objekt mithilfe von `ADB.Media.VideoMetadataKeys.MVPD`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Mediensammlungs-API

`media.pass.mvpd` in das `params` einschließen:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).
