---
title: Migration vom Standalone Media SDK zu Adobe Launch - Android
description: Erfahren Sie, wie Sie vom Media SDK zu Launch für Android migrieren.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/HawnzTGV1nsGCibAtXkl3cAB5NjO2VfUpQODm6-w-qk
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 428
ht-degree: 48%

---

# Migration vom Standalone Media SDK zu Adobe Launch – Android

>[!NOTE]
>Adobe Experience Platform Launch wurde umbenannt und umfasst eine Suite von Datenerfassungstechnologien in Experience Platform. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen vorgenommen. Eine Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).


## Konfiguration

### Standalone Media SDK

In der eigenständigen Media SDK konfigurieren Sie das Tracking in der App und übergeben es an .
Die SDK beim Erstellen des Trackers

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

1. Klicken Sie in Experience Platform Launch auf die Registerkarte [!UICONTROL Erweiterungen] für Ihre
Mobile-Eigenschaft.
1. Suchen Sie auf der [!UICONTROL Katalog] die Registerkarte Adobe Media Analytics for Audio.
und Video-Erweiterung hinzufügen und auf [!UICONTROL Installieren] klicken.
1. Konfigurieren Sie auf der Seite „Erweiterungseinstellungen“ die Tracking-Parameter.
Die Media-Erweiterung verwendet zum Tracking die konfigurierten Parameter.

![](assets/launch_config_mobile.png)

[Verwenden von Mobile-Erweiterungen](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## Erstellen von Trackern

### Standalone Media SDK

In der eigenständigen Media SDK erstellen Sie das `MediaHeartbeatConfig` manuell
und konfigurieren Sie die Tracking-Parameter. Implementieren der Delegaten-Schnittstelle, die Folgendes bereitstellt
`getQoSObject()` und `getCurrentPlaybackTime()functions.`
Erstellen Sie eine `MediaHeartbeat`-Instanz für das Tracking.

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

[Media API-Referenz - Erstellen eines Medien-Trackers](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

Bevor Sie den Tracker erstellen, sollten Sie die Medienerweiterung registrieren und
Abhängige Erweiterungen mit dem Mobile Core.

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

In der eigenständigen Media SDK übergeben Sie ein Delegate-Objekt, das die
`MediaHeartbeartDelegate` bei der Tracker-Erstellung.  Die Implementierung
sollte die neueste QoE und den neuesten Abspielkopf zurückgeben, wenn der Tracker die
`getQoSObject()`- und `getCurrentPlaybackTime()`.

### Launch-Erweiterung

Die -Implementierung sollte den aktuellen Player-Abspielkopf aktualisieren, indem sie die
`updateCurrentPlayhead` vom Tracker offen gelegte Methode. Für genaues Tracking
Sie sollten diese Methode mindestens einmal pro Sekunde aufrufen.

[Media API-Referenz - Aktuellen Player aktualisieren](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

Die -Implementierung sollte die QoE-Informationen aktualisieren, indem sie die `updateQoEObject`
Methode, die vom Tracker verfügbar gemacht wird. Wir erwarten, dass diese Methode aufgerufen wird, wann immer sie vorhanden ist
ist eine Änderung bei den Qualitätsmetriken.

[Media API-Referenz - QoE-Objekt aktualisieren](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

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
