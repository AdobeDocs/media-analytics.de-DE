---
title: Einrichten des Media SDK mit JavaScript 2.x
description: Führen Sie diese Schritte aus, um die Media SDK-Anwendung in JavaScript 2.x einzurichten.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e10f705e135cc6b9c630059596994d12fc787866
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 100%

---

# Einrichten von JavaScript 2.x{#set-up-javascript}

## Voraussetzungen

* **Gültige Konfigurationsparameter festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **`AppMeasurement` für JavaScript in Ihre Medienanwendung implementieren:** Weitere Informationen zur Adobe Mobile-SDK-Dokumentation finden Sie unter [Analytics-Implementierung mit JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de)

* **Stellen Sie die folgenden Funktionen in Ihrem Medienplayer bereit:**

   * *Eine API zum Abonnieren von Player-Ereignissen*: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * *Eine API, die Player-Informationen bereitstellt*: Diese Informationen enthalten Details wie den Mediennamen und die Abspielposition.

1. Fügen Sie Ihre [heruntergeladene](/help/sdk-implement/download-sdks.md#download-2x-sdks) Bibliothek zu Ihrem Projekt hinzu. Erstellen Sie aus Gründen der Übersichtlichkeit lokale Referenzen auf die Klassen.

   1. Erweitern Sie die heruntergeladene Datei `MediaSDK-js-v2.*.zip`.
   1. Stellen Sie sicher, dass die Datei `MediaSDK.min.js` im Verzeichnis `libs` vorhanden ist:

   1. Hosten Sie die Datei `MediaSDK.min.js`.

      Diese Core-JavaScript-Datei muss auf einem Webserver gehostet werden, auf den alle Seiten Ihrer Site zugreifen können. Sie benötigen den Pfad zu diesen Dateien für den nächsten Schritt.

   1. Referenzieren Sie `MediaSDK.min.js` auf allen Webseiten.

      Integrieren Sie `MediaSDK` für JavaScript, in dem Sie dem Tag `<head>` oder `<body>` auf jeder Seite die folgende Codezeile hinzufügen. Beispiel:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Um schnell zu überprüfen, ob die Bibliothek erfolgreich importiert wurde, instanziieren Sie die Klasse `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >Ab Version 2.1.0 entspricht das JavaScript-SDK den AMD- und CommonJS-Modulspezifikationen und `VideoHeartbeat.min.js` kann auch mit kompatiblen Module Loaders verwendet werden.

1. Erstellen Sie lokale Verweise auf die `MediaHeartbeat`-Klassen, um den Zugriff auf die APIs zu erleichtern.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Erstellen Sie eine `MediaHeartbeatConfig`-Instanz.

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

1. Implementieren Sie das `MediaHeartbeatDelegate`-Protokoll.

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

1. Erstellen Sie die `MediaHeartbeat`-Instanz.

   Verwenden Sie `MediaHeartbeatConfig` und `MediaHeartbeatDelegate`, um die `MediaHeartbeat`-Instanz zu erstellen.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass die `MediaHeartbeat`-Instanz zugänglich ist und ihre Zuweisung nicht vor Ende der Mediensitzung aufgehoben wird. Diese Instanz wird für alle der folgenden-Tracking-Ereignisse verwendet.

   >[!TIP]
   >
   >`MediaHeartbeat` erfordert eine `AppMeasurement`-Instanz, um Aufrufe an Adobe Analytics senden zu können. Beispiel für eine `AppMeasurement`-Instanz:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migrieren von JavaScript 1.x zu 2.x

In Version 2.x sind alle öffentlichen Methoden in der Klasse `ADB.va.MediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern. Außerdem sind alle Konfigurationen nun in der `ADB.va.MediaHeartbeatConfig`-Klasse konsolidiert.

Ausführliche Informationen zur Migration von 1.x zu 2.x finden Sie unter [Migration von VHL 1.x zu 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
