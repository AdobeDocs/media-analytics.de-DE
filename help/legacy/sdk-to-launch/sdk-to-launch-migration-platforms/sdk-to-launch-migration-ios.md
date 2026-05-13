---
title: Migration vom Standalone Media SDK zu Adobe Launch - iOS
description: Erfahren Sie, wie Sie für iOS vom Media SDK zu Launch migrieren.
exl-id: f70b8e1b-cb9f-4230-86b2-171bdaed4615
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/drdnQd83UXJkMKj-isUKPeIHe9xGetwY31HzHf37IEo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 60%

---

# Migration vom Standalone Media SDK zu Adobe Launch – iOS

>[!NOTE]
>Adobe Experience Platform Launch wurde umbenannt und umfasst eine Suite von Datenerfassungstechnologien in Experience Platform. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen vorgenommen. Eine Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).

## Konfiguration

### Standalone Media SDK

In der eigenständigen Media SDK konfigurieren Sie die Tracking-Konfiguration in der App,
und beim Erstellen des Trackers an SDK übergeben.

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

### Launch-Erweiterung

1. Klicken Sie unter „Experience Platform Launch“ für Ihre mobile Eigenschaft auf die Registerkarte [!UICONTROL Erweiterungen].
1. Suchen Sie auf der Registerkarte [!UICONTROL Katalog] die Erweiterung „Adobe Media Analytics for Audio and Video“ und klicken Sie auf [!UICONTROL Installieren].
1. Konfigurieren Sie auf der Seite „Erweiterungseinstellungen“ die Tracking-Parameter.
Die Media-Erweiterung verwendet zum Tracking die konfigurierten Parameter.

   ![](assets/launch_config_mobile.png)

[Konfigurieren der Media Analytics-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## Erstellen von Trackern

### Standalone Media SDK

In der eigenständigen Media SDK erstellen Sie das `ADBMediaHeartbeatConfig` manuell
und konfigurieren Sie die Tracking-Parameter. Implementieren der Delegaten-Schnittstelle, die die
`getQoSObject()` und `getCurrentPlaybackTime()functions.`

Erstellen Sie eine MediaHeartbeat-Instanz zum Tracking:

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

### Launch-Erweiterung

[Media API-Referenz - Medien-Tracker erstellen](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

Bevor Sie den Tracker erstellen, registrieren Sie die Media-Erweiterung und die abhängigen Erweiterungen beim Mobile Core.

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

Nach der Registrierung der Media-Erweiterung kann der Tracker mithilfe der folgenden API erstellt werden.
Der Tracker übernimmt automatisch die Konfiguration der Launch-Eigenschaft.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## Aktualisieren der Abspielleiste und Erlebnisqualität (QoE).

### Standalone Media SDK

In der eigenständigen Media SDK ein Delegate-Objekt, das
`ADBMediaHeartbeartDelegate` Protokoll wird während der Tracker-Erstellung übergeben.
Die Implementierung sollte die neueste QoE und den neuesten Abspielkopf zurückgeben, wenn die
Tracker ruft die Schnittstelle `getQoSObject()` und `getCurrentPlaybackTime()` auf
Methoden.

### Launch-Erweiterung

Die Implementierung sollte den aktuellen Player-Abspielkopf aktualisieren, indem sie die Variable
`updateCurrentPlayhead` vom Tracker offen gelegte Methode. Für genaues Tracking
Sie sollten diese Methode mindestens einmal pro Sekunde aufrufen.

[Media API-Referenz - Aktuellen Abspielkopf aktualisieren](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

Die -Implementierung sollte die QoE-Informationen aktualisieren, indem sie die
`updateQoEObject` vom Tracker offen gelegte Methode. Sie sollten diese Methode aufrufen
wann immer sich die Qualitätsmetriken ändern.

[Media API-Referenz - QoE-Objekt aktualisieren](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

## Weiterleiten von Standardmedien/Anzeigenmetadaten

### Standalone Media SDK

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

### Launch-Erweiterung

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
