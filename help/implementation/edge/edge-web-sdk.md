---
title: Webdaten mit dem Adobe Experience Platform Web SDK an Edge senden
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Adobe Streaming Media-Daten an Experience Platform Edge senden.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Webdaten mit dem Adobe Experience Platform Web SDK an Edge senden

Ab Version 2.20.0 können Sie mit der Komponente `streamingMedia` des Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) Daten im Zusammenhang mit Mediensitzungen auf Ihrer Website erfassen. Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen damit zusammenhängenden Ereignissen enthalten.

Nachdem die Daten erfasst wurden, können Sie sie an Adobe Experience Platform und/oder Adobe Analytics senden, um Berichte zu erstellen. Diese Funktion bietet eine umfassende Lösung zum Verfolgen und Verstehen des Verhaltens der Mediennutzung auf Ihrer Website.

Für Kunden, die das Media JS SDK verwenden, bietet das Web SDK einen Migrationspfad für den Wechsel vom Media JS SDK zum Web SDK. Gleichzeitig wird Unterstützung für vorhandene Media JS-Funktionen wie die Verarbeitung von Medienereignissen bereitgestellt.

## Voraussetzungen {#prerequisites}

Um die Komponente `streamingMedia` des Web SDK zu verwenden, müssen Sie die folgenden Voraussetzungen erfüllen:

* Bevor Sie Streaming-Mediendaten an Edge senden können, führen Sie zunächst die Schritte unter [Installieren des Streaming-Mediensammlungs-Add-ons mit Experience Platform Edge](/help/implementation/edge/implementation-edge.md) aus.
* Stellen Sie sicher, dass Sie Zugriff auf Adobe Experience Platform und/oder Adobe Analytics haben.
* Sie müssen die Web SDK-Version 2.20.0 oder höher verwenden. Informationen zur Installation der neuesten Version finden Sie in der [Übersicht zur Installation des Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) .
* Aktivieren Sie die Option **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** für den verwendeten Datastream.
* Stellen Sie sicher, dass das von Ihrem Datastream verwendete Schema die Schemafelder für die Mediensammlung enthält.
* Konfigurieren Sie die Streaming-Medien-Funktion in der Web SDK-Konfiguration, wie auf dieser Seite gezeigt, entweder über die [Tag-Erweiterung](#tag-extension) oder über die [JavaScript-Bibliothek](#library).

Führen Sie die auf dieser Seite beschriebenen Schritte aus, um Ihre Implementierung des Streaming Media Collection Add-ons von Media JS zu Web SDK zu migrieren.

### Schritt 1: Installieren des Experience Platform Web SDK

Informationen zur Installation des Web SDK in Ihren Webeigenschaften finden Sie in der [dedizierten Dokumentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) .

### Schritt 2: Konfigurieren Sie die Komponente Web SDK `streamingMedia` .

**Beispiel**

Das folgende Snippet zeigt, wie Sie die Mediensammlung in Media JS konfigurieren.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

Stattdessen müssen Sie die Komponente `streamingMedia` im Web SDK wie unten dargestellt konfigurieren.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Ausführliche Informationen zur Konfiguration finden Sie in der Dokumentation zur Web SDK `streamingMedia`-Komponente [Dokumentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) .

### Schritt 3: Abrufen der Media-Tracker-Instanz bei der Migration vom Media JS SDK

Für Kunden, die das Media JS SDK verwenden, bietet das Web SDK einen Migrationspfad für den Wechsel vom Media JS SDK zum Web SDK. Gleichzeitig wird Unterstützung für vorhandene Media JS-Funktionen wie die Verarbeitung von Medienereignissen bereitgestellt.

[!DNL Web SDK] enthält einen Befehl zum Abrufen eines Media Analytics-Trackers. Mit diesem Befehl können Sie eine Objektinstanz erstellen und dann mithilfe derselben APIs, die von der [Medien-JS-Bibliothek](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html) bereitgestellt werden, Medienereignisse verfolgen.

Vollständige Details zu den unterstützten Methoden finden Sie in der Dokumentation zu [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) .

Der nachstehende Ausschnitt zeigt, wie Sie die Media-Tracker-Instanz in Media JS abrufen.

```javascript
var tracker = ADB.Media.getInstance();
```

Verwenden Sie stattdessen den Befehl `getMediaAnalyticsTracker` im Web SDK, um dasselbe Ergebnis zu erzielen, wie unten dargestellt.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Alle Hilfsmethoden sind für das Objekt `Media` verfügbar. Die Tracker-Methoden sind in der Tracker-Instanz verfügbar, wie unten dargestellt.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
