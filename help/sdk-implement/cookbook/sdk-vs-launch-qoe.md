---
seo-title: Verstehen Sie die Unterschiede zwischen dem Start und dem Media SDK.
title: Verstehen Sie die Unterschiede zwischen dem Start und dem Media SDK.
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Verstehen Sie die Unterschiede zwischen dem Start und dem Media SDK.

## Funktionsunterschiede

* *Launch* - Launch bietet Ihnen eine Benutzeroberfläche, die Sie durch die Einrichtung, Konfiguration und Bereitstellung Ihrer webbasierten Medienverfolgungslösungen begleitet. Der Start wird unter dem dynamischen Tag-Management (DTM) verbessert.
* *Media SDK* - Das Media SDK stellt Ihnen Medienverfolgungsbibliotheken zur Verfügung, die für bestimmte Plattformen entwickelt wurden (z. B.: Android, ios usw.). Adobe empfiehlt Media SDK zur Verfolgung der Mediennutzung in Ihren mobilen Apps.

## Unterschiede bei der Trackererstellung

### Launch

Start bietet zwei Ansätze zum Erstellen der Verfolgungsinfrastruktur. Beide Ansätze verwenden die Media Analytics-Starterweiterung:

1. Verwenden Sie die Medienverfolgungs-apis auf einer Webseite.

   In diesem Szenario exportiert die Media Analytics Extension die Medienverfolgungs-apis in eine konfigurierte Variable im globalen Fensterobjekt:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Verwenden Sie die Medienverfolgungs-apis aus einer anderen Starterweiterung.

   In diesem Szenario verwenden Sie die Medienverfolgungs-apis, die von `get-instance` den und `media-heartbeat` freigegebenen Modulen offen gelegt werden.

   >[!NOTE]
   >
   >Freigegebene Module sind nicht für Webseiten verfügbar. Sie können freigegebene Module nur aus einer anderen Erweiterung verwenden.

   Erstellen Sie eine `MediaHeartbeat` Instanz mit `get-instance` dem freigegebenen Modul.
Übergeben Sie ein Delegationsobjekt, an `get-instance` das diese verfügbar `getQoSObject()``getCurrentPlaybackTime()` sind.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Greifen Sie auf `MediaHeartbeat` Konstanten über das `media-heartbeat` freigegebene Modul zu.

### Medien-SDK

1. Fügen Sie die Media Analytics-Bibliothek zu Ihrem Entwicklungsprojekt hinzu.
1. Erstellen Sie ein config-Objekt (`MediaHeartbeatConfig`).
1. Implementieren Sie das Delegationsprotokoll und stellen Sie die `getQoSObject()` Funktionen und `getCurrentPlaybackTime()` Funktionen bereit.
1. Erstellen Sie eine Media Heartbeat-Instanz (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

## Verwandte Dokumentation

### Launch

* [Startübersicht](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA-Erweiterung](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Medien-SDK

* [JS einrichten](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

