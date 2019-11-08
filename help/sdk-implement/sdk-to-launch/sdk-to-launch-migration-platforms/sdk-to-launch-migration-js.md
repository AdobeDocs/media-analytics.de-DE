---
title: Migration vom eigenständigen Media SDK zu Adobe Launch - Web (JS)
description: Anweisungen und Codebeispiele, die bei der Migration vom Media SDK zum Start helfen.
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# Migration vom eigenständigen Media SDK zu Adobe Launch - Web (JS)

## Funktionsunterschiede

* *Start* - Launch bietet eine Benutzeroberfläche, die Sie durch Einrichten, Konfigurieren und Bereitstellen Ihrer webbasierten Medienverfolgungslösungen führt. Der Start verbessert sich beim dynamischen Tag-Management (DTM).
* *Media SDK* - Das Media SDK bietet Ihnen Medienverfolgungsbibliotheken für bestimmte Plattformen (z. B.: Android, iOS usw.). Adobe empfiehlt Media SDK zur Verfolgung der Mediennutzung in Ihren mobilen Apps.

## Konfiguration

### Eigenständiges Media SDK

Im eigenständigen Media SDK konfigurieren Sie die Verfolgungskonfiguration in der App und übergeben sie an das SDK, wenn Sie den Tracker erstellen.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Zusätzlich zur `MediaHeartbeat` Konfiguration muss die Seite die `AppMeasurement` `VisitorAPI` Instanz und Instanz für die Medienverfolgung konfigurieren und übergeben, damit sie ordnungsgemäß funktioniert.

### Erweiterung starten

1. Klicken Sie unter "Experience Platform Launch"für Ihre Webeigenschaft auf die Registerkarte [!UICONTROL Erweiterungen] .
1. Suchen Sie auf der Registerkarte " [!UICONTROL Katalog] "die Erweiterung Adobe Media Analytics for Audio and Video und klicken Sie auf [!UICONTROL Installieren].
1. Konfigurieren Sie auf der Seite "Erweiterungseinstellungen"die Verfolgungsparameter.
Die Media-Erweiterung verwendet die konfigurierten Parameter für die Verfolgung.

   ![](assets/launch_config_js.png)

[Benutzerhandbuch starten - Medienerweiterung installieren und konfigurieren](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Unterschiede bei der Trackererstellung

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

[Media SDK - Trackererstellung](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

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

## Verwandte Dokumentation

### Medien-SDK

* [JS einrichten](/help/sdk-implement/setup/set-up-js.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Übersicht über den Start](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Media Analytics Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
