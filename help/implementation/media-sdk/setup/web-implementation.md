---
title: Einrichten einer Web-Implementierung für Analytics für Streaming-Medien
description: Erfahren Sie, wie Sie Adobe-Streaming-Medien für Web-Apps implementieren.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 92%

---

# Installieren des Media SDK mit JavaScript {#install-web-sdks}

Die Informationen auf dieser Seite beschreiben, wie Sie das eigenständige Web-SDK installieren und JavaScript einrichten.

Alternativ können Sie die Adobe Medium Analytics-Erweiterung verwenden, um das Adobe Streaming Media Collection Add-on zu implementieren, wie unter [Analytics mithilfe der Media Analytics-Erweiterung implementieren](/help/implementation/media-sdk/setup/web-implementation-tags.md) beschrieben.

## Voraussetzungen  {#prerequesites}

* **Abrufen gültiger Konfigurationsparameter**

  Sie können diese Parameter von einem Adobe-Support-Mitarbeiter erhalten, wenn Sie Ihr Analytics-Konto eingerichtet haben.

* **Implementierung von `AppMeasurement` und `Experience Cloud Identity Service` für JavaScript in Ihrer Medienanwendung**

  Weitere Informationen finden Sie unter [Implementieren von Analytics mit JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de) und [Implementieren des Identity-Diensts in Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=de).

* **Integrieren der folgenden APIs in Ihren Media Player**

   * *Eine API zum Abonnieren von Player-Ereignissen*: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * *Eine API, die Player-Informationen bereitstell*: Dazu gehören Informationen zur aktuellen Wiedergabe von Medien, Anzeigen und Kapiteln.

## Einrichten von JavaScript 3.x {#set-up-javascript}

1. Fügen Sie Ihre [heruntergeladene](/help/getting-started/download-sdks.md) Bibliothek zu Ihrem Projekt hinzu. Erstellen Sie aus Gründen der Übersichtlichkeit lokale Referenzen auf die Klassen.

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
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
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

Informationen zu älteren Inhalten finden Sie unter [Legacy-Implementierungen](/help/legacy/media-sdk/setup/setup-overview.md)
