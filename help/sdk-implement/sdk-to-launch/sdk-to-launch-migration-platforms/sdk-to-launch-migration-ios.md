---
seo-title: Migration vom eigenständigen Media SDK zum Adobe Launch - iOS
title: Migration vom eigenständigen Media SDK zum Adobe Launch - iOS
seo-description: Anweisungen und Codebeispiele, die bei der Migration vom Media SDK zum Launch für iOS helfen.
description: Anweisungen und Codebeispiele, die bei der Migration vom Media SDK zum Launch für iOS helfen.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# Migration vom eigenständigen Media SDK zum Adobe Launch - iOS

## Konfiguration

### Erweiterung starten

1. Klicken Sie im Experience Platform Launch für Ihre mobile Eigenschaft auf die Registerkarte [!UICONTROL Erweiterungen] .
1. Suchen Sie auf der Registerkarte " [!UICONTROL Katalog] "die Erweiterung Adobe Media Analytics for Audio and Video und klicken Sie auf [!UICONTROL Installieren].
1. Konfigurieren Sie auf der Seite "Erweiterungseinstellungen"die Verfolgungsparameter.
Die Media-Erweiterung verwendet die konfigurierten Parameter für die Verfolgung.

[Media Analytics-Erweiterung konfigurieren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

### Eigenständiges Media SDK

Im eigenständigen Media SDK konfigurieren Sie die Verfolgungskonfiguration in der App und übergeben sie beim Erstellen des Trackers an das SDK.

```objective-c
ADBMediaHeartbeatConfig *config = 
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker = 
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

## Trackererstellung

### Erweiterung starten

[Media API-Referenz - Medienverfolgung erstellen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Bevor Sie den Tracker erstellen, registrieren Sie die Medienerweiterung und die abhängigen Erweiterungen mit dem mobilen Kern.

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

Nachdem die Medienerweiterung registriert wurde, kann der Tracker mit der folgenden API erstellt werden.
Der Tracker wählt die Konfiguration automatisch aus der konfigurierten Eigenschaft launch aus.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

### Eigenständiges Media SDK

Im eigenständigen Media SDK erstellen Sie das `ADBMediaHeartbeatConfig` Objekt manuell und konfigurieren die Verfolgungsparameter. Implementieren Sie die Delegate-Schnittstelle, um die`getQoSObject()` und `getCurrentPlaybackTime()functions.`

Erstellen Sie eine MediaHeartbeat-Instanz zur Verfolgung:

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker = 
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

## Aktualisieren von Playhead und Qualität der Erlebniswerte.

### Erweiterung starten

Die Implementierung sollte die aktuelle Player-Abspielleiste durch die vom Tracker offen gelegte Methode aktualisieren`updateCurrentPlayhead` . Für eine genaue Verfolgung sollten Sie diese Methode mindestens einmal pro Sekunde aufrufen.

[Media API-Referenz - Update Current Playhead](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

Die Implementierung sollte die QoE-Informationen aktualisieren, indem die`updateQoEObject` vom Tracker offen gelegte Methode aufgerufen wird. Sie sollten diese Methode bei jeder Änderung der Qualitätsmetriken aufrufen.

[Media API-Referenz - QoE-Objekt aktualisieren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

### Eigenständiges Media SDK

Im eigenständigen Media SDK wird ein Delegate-Objekt, das das`ADBMediaHeartbeartDelegate` Protokoll implementiert, während der Trackererstellung übergeben.
Die Implementierung sollte die neueste QoE und die Abspielleiste zurückgeben, wenn der Tracker die `getQoSObject()` und die `getCurrentPlaybackTime()` Schnittstellen-Methoden aufruft.

## Übergeben von Standardmedien/Anzeigenmetadaten

### Erweiterung starten

* Standard-Medienmetadaten:

   ```objective-c
   NSDictionary *mediaObject = 
     [ACPMedia createMediaObjectWithName:@"media-name" 
               mediaId:@"media-id" 
               length:60 
               streamType:ACPMediaStreamTypeVod 
               mediaType:ACPMediaTypeVideo];
   
   NSMutableDictionary *mediaMetadata = 
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
   [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
   
   // Custom metadata keys
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   [_tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standard-Anzeigenmetadaten:

   ```objective-c
   NSDictionary* adObject = 
     [ACPMedia createAdObjectWithName:@"ad-name" 
               adId:@"ad-id" 
               position:1 
               length:15];
   
   NSMutableDictionary* adMetadata = 
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
   [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
   
   // Custom metadata keys
   [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
   ```

### Eigenständiges Media SDK

* Standard-Medienmetadaten:

   ```objective-c
   ADBMediaObject *mediaObject = 
     [ADBMediaHeartbeat createMediaObjectWithName:@"media-name" 
                        mediaId:@"media-id" 
                        length:60 
                        streamType:ADBMediaHeartbeatStreamTypeVod 
                        mediaType:ADBMediaTypeVideo];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
   [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
   [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   
   [tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standard-Anzeigenmetadaten:

   ```objective-c
   ADBMediaObject* adObject = 
     [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"] 
                        adId:[adData objectForKey:@"id"]
                        position:[[adData objectForKey:@"position"] doubleValue]
                        length:[[adData objectForKey:@"length"] doubleValue]];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = 
     [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample Advertiser" 
                     forKey:ADBAdMetadataKeyADVERTISER];
   [standardMetadata setObject:@"Sample Campaign" 
                     forKey:ADBAdMetadataKeyCAMPAIGN_ID];
   [adObject setValue:standardMetadata 
                     forKey:ADBMediaObjectKeyStandardAdMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
   [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ADBMediaHeartbeatEventAdStart 
            mediaObject:adObject 
            data:adDictionary];
   ```

