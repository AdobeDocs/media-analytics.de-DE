---
seo-title: Migration vom eigenständigen Media SDK zum Adobe Launch - Android
title: Migration vom eigenständigen Media SDK zum Adobe Launch - Android
seo-description: Anweisungen und Codebeispiele, die bei der Migration vom Media SDK zum Launch für Android helfen.
description: Anweisungen und Codebeispiele, die bei der Migration vom Media SDK zum Launch für Android helfen.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# Migration vom eigenständigen Media SDK zum Adobe Launch - Android

## Konfiguration

### Erweiterung starten

1. Klicken Sie unter "Experience Platform Launch"für Ihre mobile Eigenschaft auf die Registerkarte [!UICONTROL Erweiterungen] .
1. Suchen Sie auf der Registerkarte " [!UICONTROL Katalog] "die Erweiterung Adobe Media Analytics for Audio and Video und klicken Sie auf [!UICONTROL Installieren].
1. Konfigurieren Sie auf der Seite "Erweiterungseinstellungen"die Verfolgungsparameter.
Die Media-Erweiterung verwendet die konfigurierten Parameter für die Verfolgung.

[Mobile Extensions verwenden](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

### Eigenständiges Media SDK

Im eigenständigen Media SDK konfigurieren Sie die Verfolgung in der App und übergeben sie beim Erstellen des Trackers an das SDK.

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

## Trackererstellung

### Erweiterung starten

[Media API-Referenz - Erstellen eines Media-Trackers](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Bevor Sie den Tracker erstellen, sollten Sie die Medienerweiterung und die abhängigen Erweiterungen mit dem Mobilkern registrieren.

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

Nachdem Sie die Medienerweiterung registriert haben, erstellen Sie den Tracker mit der folgenden API.
Der Tracker wählt die Konfiguration automatisch aus der konfigurierten Eigenschaft launch aus.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

### Eigenständiges Media SDK

Im eigenständigen Media SDK erstellen Sie das `MediaHeartbeatConfig` Objekt manuell und konfigurieren die Verfolgungsparameter. Implementieren Sie die Bereitstellung`getQoSObject()` der Delegate-Schnittstelle und `getCurrentPlaybackTime()functions.`erstellen Sie eine `MediaHeartbeat` Instanz zur Verfolgung.

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

## Aktualisieren von Playhead und Qualität der Erlebniswerte.

### Erweiterung starten

Die Implementierung sollte die aktuelle Player-Abspielleiste aktualisieren, indem die`updateCurrentPlayhead` vom Tracker offen gelegte Methode aufgerufen wird. Für eine genaue Verfolgung sollten Sie diese Methode mindestens einmal pro Sekunde aufrufen.

[Media API-Referenz - Aktuellen Player aktualisieren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

Die Implementierung sollte die QoE-Informationen aktualisieren, indem die vom Tracker offen gelegte `updateQoEObject`Methode aufgerufen wird. Wir erwarten, dass diese Methode bei jeder Änderung der Qualitätsmetriken aufgerufen wird.

[Media API-Referenz - QoE-Objekt aktualisieren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

### Eigenständiges Media SDK

Im eigenständigen Media SDK übergeben Sie ein Delegate-Objekt, das die`MediaHeartbeartDelegate` Schnittstelle während der Trackererstellung implementiert.  Die Implementierung sollte die neueste QoE und die Abspielleiste zurückgeben, wenn der Tracker die`getQoSObject()` Methoden und die `getCurrentPlaybackTime()` Schnittstellenmethoden aufruft.

## Übergeben von Standardmedien/Anzeigenmetadaten

### Erweiterung starten

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

### Eigenständiges Media SDK

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


