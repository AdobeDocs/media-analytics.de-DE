---
title: Migration vom eigenständigen Media SDK zu Adobe Launch - Web (JS)
description: Erfahren Sie, wie Sie vom Media SDK zu Launch für JS migrieren.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/N4Fcbg3R9tT9cjUcaw-kcUm6h-QT8TYwatdCe1IdsaM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c069c44e-5426-4c1a-accc-8028662f2fde
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 77%

---

# Migration vom Standalone Media SDK zu Adobe Launch – Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch wurde umbenannt und umfasst eine Suite von Datenerfassungstechnologien in Experience Platform. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen vorgenommen. Eine Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).

## Funktionsunterschiede

* *Launch* – Launch bietet eine Benutzeroberfläche, die Sie durch den Einrichtungs-, Konfigurations- und Bereitstellungsvorgang für Ihre webbasierten Medien-Tracking-Lösungen führt. Launch wird durch das Dynamic Tag Management (DTM) optimiert.
* *Media SDK* – Das Media SDK bietet Ihnen Medien-Tracking-Bibliotheken für bestimmte Plattformen (z. B.: Android und iOS). Adobe empfiehlt das Media SDK zum Tracking der Mediennutzung in Ihren mobilen Apps.

## Konfiguration

### Standalone Media SDK

In der eigenständigen Media SDK konfigurieren Sie die Tracking-Konfiguration in der App
und beim Erstellen des Trackers an SDK übergeben.

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

Zusätzlich zur `MediaHeartbeat` Konfiguration muss die Seite konfigurieren und übergeben
Die `AppMeasurement` und `VisitorAPI` für das Medien-Tracking in der richtigen Reihenfolge
um richtig zu arbeiten.

### Launch-Erweiterung

1. Klicken Sie in Experience Platform Launch auf die Registerkarte [!UICONTROL Erweiterungen] für Ihre
Web-Eigenschaft.
1. Suchen Sie auf der [!UICONTROL Katalog] die Registerkarte Adobe Media Analytics for Audio and
und klicken Sie auf [!UICONTROL Installieren].
1. Konfigurieren Sie auf der Seite „Erweiterungseinstellungen“ die Tracking-Parameter.
Die Media-Erweiterung verwendet zum Tracking die konfigurierten Parameter.

   ![](assets/launch_config_js.png)

[Benutzerhandbuch starten - Installieren und Konfigurieren der Medienerweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=de#install-and-configure-the-ma-extension)

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

### Media SDK

* [Einrichten von JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [Media SDK JS-API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Launch-Übersicht](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=de)
* [Media Analytics-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=de)
