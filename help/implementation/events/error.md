---
title: Fehler
description: Signal, dass der Medienplayer auf einen Fehler gestoßen ist.
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
source-wordcount: '196'
ht-degree: 8%
---

# Fehler

Das Fehlerereignis signalisiert, dass der Media Player auf einen Fehler gestoßen ist. Beim Verfolgen eines Fehlers wird die Sitzung nicht geschlossen. Wenn der Fehler verhindert, dass die Wiedergabe fortgesetzt wird, rufen [ nach dem ](session/session-end.md) „Sitzungsende“ auf.

* **Voraussetzungen**: [Sitzungsstart](session/session-start.md)
* **Zugeordnete Metrik**: [[!UICONTROL Von Fehlern betroffene Streams]](/help/reporting/metrics/error-impacted-streams.md)

Die `errorDetails.source`-Eigenschaft akzeptiert nur zwei Werte: `player` (Fehler, die vom Media-Player stammen) und `external` (Fehler von einer externen Quelle wie einem CDN oder Netzwerk).

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Rufen Sie [`sendEvent`](https://experienceleague.adobe.com/de/docs/experience-platform/collection/js/commands/sendevent/overview) mit `eventType: "media.error"` und den erforderlichen `errorDetails` auf:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

`trackError` mit einer Fehler-ID-Zeichenfolge aufrufen.

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

`trackError` mit einer Fehler-ID-Zeichenfolge aufrufen.

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Roku Edge]

Rufen Sie `sendMediaEvent` mit `eventType: "media.error"` und den erforderlichen `errorDetails` auf:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

>[!TAB Media Edge-API]

Rufen Sie den [error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/)-Endpunkt mit dem erforderlichen `errorDetails` auf:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
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

`trackError` mit einer Fehler-ID-Zeichenfolge aufrufen:

```javascript
tracker.trackError("media-error-001");
```

>[!TAB Chromecast]

`trackError` mit einer Fehler-ID-Zeichenfolge aufrufen:

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB Roku 2.x]

Rufen Sie `mediaTrackError` mit einer Fehler-ID und der Fehlerquelle auf. Verwenden Sie die `ERROR_SOURCE_PLAYER` für Player-Fehler:

```brightscript
adb = ADBMobile()
adb.mediaTrackError("media-error-001", adb.ERROR_SOURCE_PLAYER)
```

>[!TAB Media Collection API]

Senden eines `error` POST an den [events-Endpunkt](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```

>[!ENDTABS]
