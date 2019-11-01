---
title: JavaScript einrichten
description: Einrichtung der Media SDK-Anwendung für die Implementierung auf JavaScript.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# JavaScript einrichten{#set-up-javascript}

## Voraussetzungen

* **Abrufen gültiger Konfigurationsparameter** Diese Parameter können von einem Adobe-Kundenbetreuer abgerufen werden, nachdem Sie Ihr Analytics-Konto eingerichtet haben.
* **Implementierung`AppMeasurement`für JavaScript in Ihre Medienanwendung** Weitere Informationen zur Adobe Mobile SDK-Dokumentation finden Sie unter [Implementieren von Analytics mit JavaScript.](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **Stellen Sie in Ihrem Medienplayer folgende Funktionen bereit:**

   * *Eine API, um Player-Ereignisse zu abonnieren:* Die Medien-SDK erfordert, dass Sie einige einfache APIs aufrufen, wenn Ereignisse in Ihrem Player auftreten.
   * *Eine API, die Playerinformationen bereitstellt:* Diese Informationen enthalten Details wie z. B. Medienname und Abspielposition.

1. Fügen Sie Ihre [heruntergeladene](/help/sdk-implement/download-sdks.md#download-2x-sdks) Bibliothek zu Ihrem Projekt hinzu. Erstellen Sie aus Gründen der Übersichtlichkeit lokale Referenzen auf die Klassen.

   1. Erweitern Sie die `MediaSDK-js-v2.*.zip` heruntergeladene Datei.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      Diese Core-JavaScript-Datei muss auf einem Webserver gehostet werden, der für alle Seiten Ihrer Website zugänglich ist. Für den nächsten Schritt benötigen Sie den Pfad zu diesen Dateien.

   1. Referenzieren Sie `MediaSDK.min.js` auf allen Webseiten.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. Beispiel:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Um schnell zu überprüfen, ob die --Bibliothek erfolgreich importiert wurde, instanziieren Sie die Klasse `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. Erstellen Sie lokale Verweise auf die `MediaHeartbeat`-Klassen, um den Zugriff auf die APIs zu erleichtern.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

   In diesem Abschnitt erhalten Sie Informationen zu den `MediaHeartbeat`-Konfigurationsparametern und zum Festlegen der richtigen Konfigurationswerte für die `MediaHeartbeat`-Instanz, um Ereignisse genau zu verfolgen.

   Hier finden Sie eine Beispielinitialisierung für `MediaHeartbeatConfig`:

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. Implement the `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. Diese Instanz wird für alle der folgenden-Tracking-Ereignisse verwendet.

   >[!TIP]
   >
   >`MediaHeartbeat` erfordert eine Instanz von , `AppMeasurement` um Aufrufe an Adobe Analytics zu senden. Beispiel für eine `AppMeasurement`-Instanz:

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## Migration von Version 1.x auf 2.x in JavaScript

In Version 2.x sind alle öffentlichen Methoden in der Klasse `ADB.va.MediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern. Außerdem sind alle Konfigurationen nun in der `ADB.va.MediaHeartbeatConfig`-Klasse konsolidiert.

Ausführliche Informationen zur Migration von 1.x zu 2.x finden Sie unter [Migration von VHL 1.x zu 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
