---
title: „Migration vom Standalone Media SDK zu Adobe Launch – Web (JS)“
description: Erfahren Sie, wie Sie vom Media SDK zu Launch für JS migrieren.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ceef739641ae07ea05314fb2bc23028de6ee5efb
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 93%

---

# Migration vom Standalone Media SDK zu Adobe Launch – Web (JS)

## Funktionsunterschiede

* *Launch* – Launch bietet eine Benutzeroberfläche, die Sie durch den Einrichtungs-, Konfigurations- und Bereitstellungsvorgang für Ihre webbasierten Medien-Tracking-Lösungen führt. Launch wird durch das Dynamic Tag Management (DTM) optimiert.
* *Media SDK* – Das Media SDK bietet Ihnen Medien-Tracking-Bibliotheken für bestimmte Plattformen (z. B.: Android und iOS). Adobe empfiehlt das Media SDK zum Tracking der Mediennutzung in Ihren mobilen Apps.

## Konfiguration

### Standalone Media SDK

Im Standalone Media SDK konfigurieren Sie das Tracking in der App und diese Konfiguration wird beim Erstellen des Trackers an das SDK übergeben.

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

Zusätzlich zur `MediaHeartbeat`-Konfiguration muss auf der Seite die `AppMeasurement` und `VisitorAPI` -Instanz für das Medien-Tracking konfiguriert und bereitgestellt werden, damit die Seite ordnungsgemäß funktioniert.

### Launch-Erweiterung

1. Klicken Sie unter „Experience Platform Launch“ für Ihre Web-Eigenschaft auf die Registerkarte [!UICONTROL Erweiterungen].
1. Suchen Sie auf der Registerkarte [!UICONTROL Katalog] die Erweiterung „Adobe Media Analytics for Audio and Video“ und klicken Sie auf [!UICONTROL Installieren].
1. Konfigurieren Sie auf der Seite „Erweiterungseinstellungen“ die Tracking-Parameter.
Die Media-Erweiterung verwendet zum Tracking die konfigurierten Parameter.

   ![](assets/launch_config_js.png)

[Launch-Benutzerhandbuch – Installieren und Konfigurieren der Media-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## Unterschiede bei der Tracker-Erstellung

### Media SDK

1. Fügen Sie Ihrem Projekt die Media Analytics-Bibliothek hinzu.
1. Erstellen Sie ein config-Objekt (`MediaHeartbeatConfig`).
1. Implementieren Sie das Delegate-Protokoll, das die Funktionen `getQoSObject()` und `getCurrentPlaybackTime()` verfügbar macht.
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

<!--  Dead Link - from 2019 - can't locate where this should go
[Media SDK - Tracker Creation](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Launch

Launch bietet zwei Methoden zum Erstellen der Tracking-Infrastruktur. Beide Methoden verwenden die Media Analytics Launch-Erweiterung:

1. Verwenden der Medien-Tracking-APIs einer Webseite

   In diesem Szenario exportiert die Media Analytics-Erweiterung die Medien-Tracking-APIs in eine konfigurierte Variable im globalen Fensterobjekt:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Verwenden der Medien-Tracking-APIs einer anderen Launch-Erweiterung

   In diesem Szenario verwenden Sie die Medien-Tracking-APIs, die von den Shared Modules `get-instance` und `media-heartbeat` bereitgestellt werden.

   >[!NOTE]
   >
   >Shared Modules können nicht auf Webseiten verwendet werden. Sie werden nur in anderen Erweiterungen zur Verfügung gestellt.

   Erstellen Sie eine `MediaHeartbeat`-Instanz mit dem Shared Module `get-instance`.
Übergeben Sie ein Delegate-Objekt an `get-instance`, das die Funktionen `getQoSObject()` und `getCurrentPlaybackTime()` verfügbar macht.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Greifen Sie auf die `MediaHeartbeat`-Konstanten über das Shared Module `media-heartbeat` zu.

## Verwandte Dokumentation

### Medien-SDK

* [Einrichten von JavaScript 2.x](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [Einrichten von JavaScript 3.x](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Launch-Übersicht](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Media Analytics-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
