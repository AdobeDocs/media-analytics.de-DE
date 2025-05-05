---
title: Senden von Web-Daten an Edge mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit der Adobe Experience Platform Web SDK Adobe-Streaming-Mediendaten an Experience Platform Edge senden.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Senden von Web-Daten an Edge mit Adobe Experience Platform Web SDK

Ab Version 2.20.0 können Sie mit der `streamingMedia` der Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/home) Daten zu Mediensitzungen auf Ihrer Website erfassen. Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen zugehörigen Ereignissen enthalten.

Nachdem die Daten erfasst wurden, können Sie sie an Adobe Experience Platform und/oder Adobe Analytics senden, um Berichte zu generieren. Diese Funktion bietet eine umfassende Lösung zum Tracking und zum Verständnis des Medienkonsumverhaltens auf Ihrer Website.

Für Kunden, die die Media JS-SDK verwenden, bietet Web SDK einen Migrationspfad, um von Media JS-SDK zu Web SDK zu wechseln, wobei bestehende Media JS-Funktionen, z. B. die Verarbeitung von Medienereignissen, unterstützt werden.

## Voraussetzungen {#prerequisites}

Um die `streamingMedia` von Web SDK verwenden zu können, müssen Sie die folgenden Voraussetzungen erfüllen:

* Bevor Sie Streaming-Mediendaten an Edge senden können, führen Sie zunächst die Schritte in [Installieren der Streaming-Mediensammlung mit Experience Platform Edge](/help/implementation/edge/implementation-edge.md) aus.
* Stellen Sie sicher, dass Sie Zugriff auf Adobe Experience Platform und/oder Adobe Analytics haben.
* Sie müssen Web SDK Version 2.20.0 oder höher verwenden. Siehe [Web SDK-Installation - Übersicht](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/install/overview), um zu erfahren, wie Sie die neueste Version installieren.
* Aktivieren Sie **[[!UICONTROL Option &#x200B;]](https://experienceleague.adobe.com/de/docs/experience-platform/datastreams/configure)** Media Analytics) für den verwendeten Datenstrom.
* Stellen Sie sicher, dass das von Ihrem Datenstrom verwendete Schema die Schemafelder der Mediensammlung enthält.
* Konfigurieren Sie die Funktion für Streaming-Medien in der Web-SDK-Konfiguration, wie auf dieser Seite gezeigt, entweder über die [Tag-Erweiterung](#tag-extension) oder über die [JavaScript-Bibliothek](#library).

Führen Sie die auf dieser Seite beschriebenen Schritte aus, um Ihre Implementierung der Streaming-Mediensammlung von Media JS zu Web SDK zu migrieren.

### Schritt 1: Installieren von Experience Platform Web SDK

In der [dedizierten Dokumentation](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/install/overview) erfahren Sie, wie Sie Web SDK in Ihren Web-Eigenschaften installieren.

### Schritt 2: Konfigurieren Sie die Web SDK-`streamingMedia`.

**Beispiel**

Der folgende Ausschnitt zeigt, wie Sie die Mediensammlung in Media JS konfigurieren würden.

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

Stattdessen müssen Sie die `streamingMedia` wie unten dargestellt in der Web-SDK konfigurieren.

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

Vollständige Details zur Konfiguration finden Sie in [ Dokumentation ](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/commands/configure/streamingmedia) Web SDK-`streamingMedia` .

### Schritt 3: Abrufen der Media Tracker-Instanz bei der Migration von der Media JS-SDK

Für Kunden, die die Media JS-SDK verwenden, bietet Web SDK einen Migrationspfad, um von Media JS-SDK zu Web SDK zu wechseln, wobei bestehende Media JS-Funktionen, z. B. die Verarbeitung von Medienereignissen, unterstützt werden.

[!DNL Web SDK] enthält einen Befehl zum Abrufen eines Media Analytics-Trackers. Sie können diesen Befehl verwenden, um eine Objektinstanz zu erstellen, und dann mit denselben APIs wie in der [Media JS Library](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html) Medienereignisse verfolgen.

In der [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker)-Dokumentation finden Sie vollständige Details zu den unterstützten Methoden.

Der folgende Ausschnitt zeigt, wie Sie die Medien-Tracker-Instanz in Media JS abrufen würden.

```javascript
var tracker = ADB.Media.getInstance();
```

Verwenden Sie stattdessen den Befehl `getMediaAnalyticsTracker` in Web SDK, um dasselbe Ergebnis zu erzielen, wie unten dargestellt.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Alle Hilfsmethoden sind für das `Media` verfügbar. Die Tracker-Methoden sind auf der Tracker-Instanz verfügbar, wie unten dargestellt.

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
