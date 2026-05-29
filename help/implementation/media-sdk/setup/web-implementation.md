---
title: Einrichten einer Web-Implementierung für Analytics für Streaming-Medien
description: Erfahren Sie, wie Sie Adobe-Streaming-Medien für Web-Apps implementieren.
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
TQID: https://experienceleague.adobe.com/UBY26SeGZbGWHjwOm6-YZNET8fe5Gvvco7aIZ9Z7rZg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 78%

---

# Installieren von Media SDK mithilfe von JavaScript {#install-web-sdks}

>[!IMPORTANT]
>
>Auf dieser Seite wird die reine Analytics-Implementierung von JavaScript Web SDK beschrieben. Die empfohlene Implementierung finden Sie unter [Implementieren von Streaming-Medien mit der Edge Network](/help/implementation/edge/edge-web-sdk.md).

Die Informationen auf dieser Seite beschreiben, wie Sie das eigenständige Web-SDK installieren und JavaScript einrichten.

Alternativ können Sie die Adobe Media Analytics-Erweiterung verwenden, um Streaming-Medien-Services zu implementieren, wie unter [Installieren von Streaming-Medien-Services mithilfe der Media Analytics-Erweiterung](/help/implementation/media-sdk/setup/web-implementation-tags.md) beschrieben.

## Voraussetzungen {#prerequesites}

* **Abrufen gültiger Konfigurationsparameter**

  Sie können diese Parameter von einem Adobe-Support-Mitarbeiter erhalten, wenn Sie Ihr Analytics-Konto eingerichtet haben.

* **Implementierung von `AppMeasurement` und `Experience Cloud Identity Service` für JavaScript in Ihrer Medienanwendung**

  Weitere Informationen finden Sie unter [Analytics mit JavaScript implementieren](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de) und [Besucheridentifizierung mit AppMeasurement](https://experienceleague.adobe.com/de/docs/analytics/implementation/id/appmeasurement).

* **Integrieren der folgenden APIs in Ihren Media Player**

   * *Eine API zum Abonnieren von Player-Ereignissen*: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * *Eine API, die Player-Informationen bereitstell*: Dazu gehören Informationen zur aktuellen Wiedergabe von Medien, Anzeigen und Kapiteln.

## Einrichten von JavaScript 3.x {#set-up-javascript}

1. Fügen Sie Ihre [heruntergeladene](/help/getting-started/download-sdks.md) Bibliothek zu Ihrem Projekt hinzu. Erstellen Sie aus Gründen der Übersichtlichkeit lokale Referenzen auf die Klassen.

   1. Erweitern Sie die heruntergeladene Datei `MediaSDK-js-v3*.zip`.
   1. Stellen Sie sicher, dass die Datei `MediaSDK.js` im Verzeichnis `libs` vorhanden ist.

   1. Hosten Sie die Datei `MediaSDK.js`.

      Diese Core-JavaScript-Datei muss auf einem Webserver gehostet werden, auf den alle Seiten Ihrer Site zugreifen können. Sie benötigen den Pfad zu diesen Dateien für den nächsten Schritt.

   1. Referenzieren Sie `MediaSDK.js` auf allen Web-Seiten.

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

Ausführliche Informationen zur Migration von 2.x zu 3.x finden Sie unter [Migration von JS SDK 2.x zu 3.x](/help/implementation/media-sdk/setup/migrate-js-2x-to-3x.md).
