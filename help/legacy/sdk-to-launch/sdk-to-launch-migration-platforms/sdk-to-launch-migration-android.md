---
title: „Migration vom Standalone Media SDK zu Adobe Launch – Android“
description: Erfahren Sie, wie Sie vom Media SDK zu Launch für Android migrieren.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 100%

---

# Migration vom Standalone Media SDK zu Adobe Launch – Android

>[!NOTE]
>Adobe Experience Platform Launch wurde umbenannt und umfasst eine Suite von Datenerfassungstechnologien in Experience Platform. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen vorgenommen. Eine Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).


## Konfiguration

### Standalone Media SDK

Sie konfigurieren im Standalone Media SDK das Tracking in der App, das beim Erstellen des Trackers an das SDK übergeben wird.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider";
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### Launch-Erweiterung

1. Klicken Sie unter „Experience Platform Launch“ für Ihre mobile Eigenschaft auf die Registerkarte [!UICONTROL Erweiterungen].
1. Suchen Sie auf der Registerkarte [!UICONTROL Katalog] die Erweiterung „Adobe Media Analytics for Audio and Video“ und klicken Sie auf [!UICONTROL Installieren].
1. Konfigurieren Sie auf der Seite „Erweiterungseinstellungen“ die Tracking-Parameter.
Die Media-Erweiterung verwendet zum Tracking die konfigurierten Parameter.

![](assets/launch_config_mobile.png)

[Verwendung mobiler Erweiterungen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Erstellen von Trackern

### Standalone Media SDK

Im Standalone Media SDK erstellen Sie das Objekt `MediaHeartbeatConfig` manuell und konfigurieren die Tracking-Parameter. Implementieren Sie die Delegate-Schnittstelle, auf der `getQoSObject()` und `getCurrentPlaybackTime()functions.` verfügbar sind. Erstellen Sie eine `MediaHeartbeat`-Instanz zum Tracking.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider";
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>);
    }

    @Override
    public Double getCurrentPlaybackTime() {
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>;
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### Launch-Erweiterung

[Media API-Referenz – Erstellen eines Medien-Trackers](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Bevor Sie den Tracker erstellen, registrieren Sie die Media-Erweiterung und die abhängigen Erweiterungen beim Mobile Core.

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

Nachdem Sie die Media-Erweiterung registriert haben, erstellen Sie den Tracker mithilfe der folgenden API.
Der Tracker übernimmt automatisch die Konfiguration der Launch-Eigenschaft.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## Aktualisieren der Abspielleiste und Erlebnisqualität (QoE).

### Standalone Media SDK

Im Standalone Media SDK übergeben Sie ein Delegate-Objekt, das die `MediaHeartbeartDelegate`-Schnittstelle während der Tracker-Erstellung implementiert.  Durch die Implementierung werden die aktuellen QoE- und die Abspielleistendaten zurückgegeben, wenn der Tracker die Schnittstellen-Methoden `getQoSObject()` und `getCurrentPlaybackTime()` aufruft.

### Launch-Erweiterung

Durch die Implementierung wird die aktuelle Player-Abspielleiste aktualisiert, indem die `updateCurrentPlayhead`-Methode aufgerufen wird, die vom Tracker verfügbar gemacht wird. Für ein exaktes Tracking sollten Sie diese Methode mindestens einmal pro Sekunde aufrufen.

[Media API-Referenz – Aktuellen Player aktualisieren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

Durch die Implementierung sollte die QoE-Informationen aktualisiert werden, indem die vom Tracker verfügbar gemachte `updateQoEObject`-Methode aufgerufen wird. Diese Methode wird bei jeder Änderung der Qualitätsmetriken aufgerufen.

[Media API-Referenz – QoE-Objekt aktualisieren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Weiterleiten von Standardmedien/Anzeigenmetadaten

### Standalone Media SDK

* Standard-Medienmetadaten:

   ```java
   MediaObject mediaInfo =
     MediaHeartbeat.createMediaObject("media-name",
                                      "media-id",
                                      60D,
                                      MediaHeartbeat.StreamType.VOD,
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata =
     new HashMap<String, String>();
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE,
                             "Sample Episode");
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW,
                             "Sample Show");
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON,
                             "Sample Season");
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata,
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Standard-Anzeigenmetadaten:

   ```java
   MediaObject adInfo =
     MediaHeartbeat.createAdObject("ad-name",
                                   "ad-id",
                                   1L,
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata =
     new HashMap<String, String>();
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER,
                          "Sample Advertiser");
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID,
                          "Sample Campaign");
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata,
                   standardAdMetadata);
   
   HashMap<String, String> adMetadata =
     new HashMap<String, String>();
   adMetadata.put("affiliate",
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart,
                      adObject,
                      adMetadata);
   ```

### Launch-Erweiterung

* Standard-Medienmetadaten:

   ```java
   HashMap<String, Object> mediaObject =
     Media.createMediaObject("media-name",
                             "media-id",
                             60D,
                             MediaConstants.StreamType.VOD,
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata =
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE,
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW,
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Standard-Anzeigenmetadaten:

   ```java
   HashMap<String, Object> adObject =
     Media.createAdObject("ad-name",
                          "ad-id",
                          1L,
                          15D);
   HashMap<String, String> adMetadata =
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER,
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID,
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate",
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart,
                       adObject,
                       adMetadata);
   ```
