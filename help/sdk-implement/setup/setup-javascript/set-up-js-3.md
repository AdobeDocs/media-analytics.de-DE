---
title: Einrichten von JavaScript 3.x
description: Einrichten der Media SDK-Anwendung für die Implementierung auf JavaScript 3.x.
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '398'
ht-degree: 100%

---

# Einrichten von JavaScript 3.x {#set-up-javascript}

## Voraussetzungen

* **Gültige Konfigurationsparameter festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **Implementieren Sie `AppMeasurement` und `Experience Cloud Identity Service` für JavaScript in Ihrer Medienanwendung**
Weitere Informationen finden Sie unter [Analytics-Implementierung mit JavaScript](https://docs.adobe.com/content/help/de-DE/analytics/implementation/js/overview.html) und [Implementieren des Experience Cloud-Identitätsdiensts](https://docs.adobe.com/content/help/de-DE/id-service/using/implementation/setup-analytics.html).

* **Stellen Sie die folgenden Funktionen in Ihrem Medienplayer bereit:**

   * *Eine API zum Abonnieren von Player-Ereignissen*: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * *Eine API, die Player-Informationen bereitstellt*: Dazu gehören Informationen zur aktuellen Wiedergabe von Medien, Anzeigen und Kapiteln.

1. Fügen Sie Ihre [heruntergeladene](/help/sdk-implement/download-sdks.md#download-3x-sdks) Bibliothek zu Ihrem Projekt hinzu. Erstellen Sie aus Gründen der Übersichtlichkeit lokale Referenzen auf die Klassen.

   1. Erweitern Sie die heruntergeladene Datei `MediaSDK-js-v3*.zip`.
   1. Stellen Sie sicher, dass die Datei `MediaSDK.js` im Verzeichnis `libs` vorhanden ist.

   1. Hosten Sie die Datei `MediaSDK.js`.

      Diese Core-JavaScript-Datei muss auf einem Webserver gehostet werden, auf den alle Seiten Ihrer Site zugreifen können. Sie benötigen den Pfad zu diesen Dateien für den nächsten Schritt.

   1. Referenzieren Sie `MediaSDK.js` auf allen Webseiten.

      Integrieren Sie `MediaSDK` für JavaScript, in dem Sie dem Tag `<head>` oder `<body>` auf jeder Seite die folgende Codezeile hinzufügen. Beispiel:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Um schnell zu überprüfen, ob die Bibliothek erfolgreich importiert wurde, prüfen Sie, ob `ADB.Media` für das Window-Objekt exportiert wurde.

      >[!NOTE]
      >
      >Das JavaScript-SDK entspricht den AMD- und CommonJS-Modulspezifikationen und `MediaSDK.js` kann auch mit kompatiblen Module Loaders verwendet werden.

1. Erstellen Sie eine Instanz von `AppMeasurement` und konfigurieren Sie `visitor`.

   Für die Media SDK-Konfiguration muss eine Instanz von `AppMeasurement` mit `visitor` konfiguriert sein.

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. Konfigurieren von Media SDK

   Media SDK sollte einmal pro Webseite konfiguriert werden und die Konfiguration gilt für alle erstellten Trackerinstanzen.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) verwendet für das Tracking von Medien die Mediensammlungs-API, die sich vom HB-Endpunkt unterscheidet, der in 2.x-SDKs verwendet wird. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um weitere Informationen zu erhalten.

   Hier finden Sie eine Beispielinitialisierung für `MediaConfig`:

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. Erstellen Sie die `MediaTracker`-Instanz.

   Nach dem Konfigurieren von Media SDK können Trackerinstanzen für das Tracking von Medieninhalten mit der `getInstance`-API erstellt werden.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass die `tracker`-Instanz zugänglich ist und ihre Zuweisung nicht vor Ende der Mediensitzung aufgehoben wird. Diese Instanz wird für das Tracking aller folgenden Ereignisse für diese Sitzung verwendet.

## Migrieren von JavaScript 2.x zu 3.x

Ausführliche Informationen zur Migration von 2.x zu 3.x finden Sie unter [Migration von 2.x zu 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)
