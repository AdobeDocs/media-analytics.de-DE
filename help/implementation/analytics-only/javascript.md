---
title: Einrichten von JavaScript für Streaming-Medien
description: Installieren und konfigurieren Sie Media SDK für JavaScript (3.x) für reine Analytics-Streaming-Medienimplementierungen.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%

---

# Einrichten von JavaScript für Streaming-Medien

Media SDK für JavaScript (3.x) sendet Streaming-Mediendaten direkt an Adobe Analytics. Auf dieser Seite wird die manuelle Installation von JavaScript beschrieben. Informationen zum Bereitstellen der SDK über Tags finden Sie unter [Einrichten der Tag-Erweiterung für Media Analytics](javascript-tags.md). Bei neuen Implementierungen sollten Sie die Verwendung von [Web SDK](/help/implementation/edge/web-sdk.md) erwägen, um Daten über einen Edge Network-Datenstrom an Adobe Analytics zu senden.

* **Voraussetzungen**:
   * Schließen Sie die [Nur Analytics-Implementierung - Übersicht](overview.md) ab.
   * Implementieren Sie [AppMeasurement](https://experienceleague.adobe.com/de/docs/analytics/implementation/js/overview) und den [Besucher-ID-Service](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement).
   * [Laden Sie die Media SDK für JavaScript herunter](/help/getting-started/download-sdks.md).

## Installieren und Konfigurieren von SDK

1. Host `MediaSDK.js` (aus dem heruntergeladenen `libs`) auf einem Webserver, auf den alle Seiten zugreifen können, und verweisen auf jeder Seite darauf:

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. Konfigurieren Sie die Media SDK einmal pro Seite und übergeben Sie die `appMeasurement`-Instanz, die Sie als Voraussetzung eingerichtet haben:

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >Die `mediaConfig.trackingServer` ist Ihr **Mediensammlungs-Server** (z. B. `[namespace].hb-api.omtrdc.net`). Dieser Sammlungsserver unterscheidet sich vom Analytics-Tracking-Server, der in der AppMeasurement-Instanz konfiguriert ist.

1. Erstellen Sie eine Tracker-Instanz mit `getInstance`. Instanz für die gesamte Mediensitzung verfügbar halten:

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## Medien-Events tracken

Verfolgen Sie bei erstelltem Tracker jedes Medienereignis mit der entsprechenden Tracker-Methode. Die **Aufrufe finden Sie auf der Registerkarte** Media SDK JS 3.x[ auf jeder Seite mit ](/help/implementation/events/overview.md) Ereignissen und [Variablen](/help/implementation/variables/overview.md) .

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für reine Analytics-Implementierungen einrichten](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [API-Referenz zu Media SDK für JavaScript 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [Migration von JS SDK 2.x zu 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [Einrichten der Tag-Erweiterung „Media Analytics“](javascript-tags.md)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
