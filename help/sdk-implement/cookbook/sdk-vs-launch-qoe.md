---
seo-title: Unterschiede zwischen Start und Media SDK verstehen
title: Unterschiede zwischen Start und Media SDK verstehen
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Unterschiede zwischen Start und Media SDK verstehen

## Funktionsunterschiede

* *Start* - Launch bietet eine Benutzeroberfläche, die Sie durch Einrichten, Konfigurieren und Bereitstellen Ihrer webbasierten Medienverfolgungslösungen führt. Der Start verbessert sich beim dynamischen Tag-Management (DTM).
* *Media SDK* - Das Media SDK bietet Ihnen Medienverfolgungsbibliotheken für bestimmte Plattformen (z. B.: Android, iOS usw.). Adobe empfiehlt Media SDK zur Verfolgung der Mediennutzung in Ihren mobilen Apps.

## Unterschiede bei der Trackererstellung

### Launch

Launch bietet zwei Ansätze zum Erstellen der Tracking-Infrastruktur. Beide Ansätze verwenden die Media Analytics Launch Extension:

1. Verwenden Sie die Medienverfolgungs-APIs einer Webseite.

   In diesem Szenario exportiert die Media Analytics-Erweiterung die Medienverfolgungs-APIs in eine konfigurierte Variable im globalen Fensterobjekt:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Verwenden Sie die Medienverfolgungs-APIs einer anderen Starterweiterung.

   In diesem Szenario verwenden Sie die Medienverfolgungs-APIs, die von den `get-instance` und `media-heartbeat` freigegebenen Modulen bereitgestellt werden.

   >[!NOTE]
   >
   >Freigegebene Module sind nicht für die Verwendung auf Webseiten verfügbar. Sie können freigegebene Module nur von einer anderen Erweiterung verwenden.

   Erstellen Sie eine `MediaHeartbeat` Instanz mit dem `get-instance` Shared Module.
Übergeben Sie ein Delegate-Objekt an `get-instance` das `getQoSObject()` und `getCurrentPlaybackTime()` Funktionen verfügbar macht.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Zugriff auf `MediaHeartbeat` Konstanten über das `media-heartbeat` freigegebene Modul.

### Medien-SDK

1. Fügen Sie Ihrem Entwicklungsprojekt die Medienanalysebibliothek hinzu.
1. Erstellen Sie ein config-Objekt (`MediaHeartbeatConfig`).
1. Implementieren Sie das Delegate-Protokoll, und stellen Sie die `getQoSObject()` Funktionen und `getCurrentPlaybackTime()` Funktionen offen.
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

* [Übersicht über den Start](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA-Erweiterung](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Medien-SDK

* [JS einrichten](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

