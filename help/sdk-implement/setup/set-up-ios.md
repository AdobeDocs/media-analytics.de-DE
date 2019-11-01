---
title: Einrichten von iOS
description: Einrichtung der Media SDK-Anwendung für die Implementierung unter iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS einrichten{#set-up-ios}

## Voraussetzungen

* **Abrufen gültiger Konfigurationsparameter für das Media SDK** Diese Parameter können Sie von einem Adobe-Kundenbetreuer erhalten, nachdem Sie Ihr Analytics-Konto eingerichtet haben.
* **Implementieren von ADBMobile für iOS in Ihre Anwendung** Weitere Informationen zur Adobe Mobile SDK-Dokumentation finden Sie unter [iOS SDK 4.x für Experience Cloud-Lösungen.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >Seit iOS 9 hat Apple eine Funktion namens App Transport Security (ATS) eingeführt. Diese Funktion soll die Netzwerksicherheit steigern, indem sie gewährleistet, dass Ihre Anwendungen nur branchenübliche Protokolle und Chiffren verwenden. Die Funktion ist standardmäßig aktiviert, Ihnen stehen jedoch einige Konfigurationsoptionen für die Arbeit mit ATS zur Verfügung. Weitere Informationen zu ATS finden Sie unter [App Transport Security.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **Stellen Sie in Ihrem Medienplayer folgende Funktionen bereit:**

   * _Eine API, um Player-Ereignisse zu abonnieren:_ Die Medien-SDK erfordert, dass Sie einige einfache APIs aufrufen, wenn Ereignisse in Ihrem Player auftreten.
   * _Eine API, die Playerinformationen bereitstellt:_ Diese Informationen enthalten Details wie z. B. Medienname und Abspielposition.

## SDK-Implementierung

1. Fügen Sie Ihr [heruntergeladenes](/help/sdk-implement/download-sdks.md#download-2x-sdks) Medien-SDK zu Ihrem Projekt hinzu.

   1. Stellen Sie sicher, dass die folgenden Softwarekomponenten im Verzeichnis `libs` vorhanden sind:

      * `ADBMediaHeartbeat.h`: Die Objective-C-Header-Datei, die für iOS Heartbeat-Tracking-APIs verwendet wird.
      * `ADBMediaHeartbeatConfig.h`: Die Objective-C-Header-Datei für die SDK-Konfiguration.
      * `MediaSDK.a`: Eine Bitcode-fähige Fat Binary, die die Bibliotheks-Builds für iOS-Geräte (armv7, armv7s, arm64) und Simulatoren (i386 und x86_64) enthält.

         Diese Binärdatei sollte verknüpft werden, wenn das Ziel für eine iOS-App vorgesehen ist.

      * `MediaSDK_TV.a`: Eine Bitcode-fähige Fat Binary, die die Bibliotheks-Builds für neue Apple TV-Geräte (arm64) und Simulatoren (x86_64) enthält.

         Diese Binärdatei sollte verknüpft werden, wenn das Ziel eine Apple TV-(tvOS-)App ist.
   1. Bibliothek zu Ihrem Projekt hinzufügen:

      1. Starten Sie die XCode IDE und öffnen Sie die App.
      1. Ziehen Sie im **[!UICONTROL Project Navigator]** (Projektnavigator) das Verzeichnis `libs` per Drag-and-drop in das Projekt.

      1. Stellen Sie sicher, dass das Kontrollkästchen **[!UICONTROL Copy Items if Needed]** (Elemente bei Bedarf kopieren) aktiviert ist, die Option **[!UICONTROL Create Groups](Gruppen erstellen) ausgewählt wurde und keines der Kontrollkästchen in** Add to Target] (Zu Ziel hinzufügen) aktiviert ist.**[!UICONTROL **

         ![](assets/choose-options_ios.png)

      1. Klicken Sie auf **[!UICONTROL Fertigstellen]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. Verknüpfen Sie im Bereich **[!UICONTROL Verknüpfte Frameworks]** und **[!UICONTROL Bibliotheken]** im Tab **[!UICONTROL Allgemein]** die erforderlichen Frameworks und Bibliotheken.

         **iOS-App-Ziele:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Apple TV (tvOS)-Targets:**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Überprüfen Sie, ob die App fehlerfrei erstellt wird.




1. Importieren Sie die Bibliothek.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a `ADBMediaHeartbeatConfig` instance.

   In diesem Abschnitt erhalten Sie Informationen zu den `MediaHeartbeat`-Konfigurationsparametern und zum Festlegen der richtigen Konfigurationswerte für die `MediaHeartbeat`-Instanz, um Ereignisse genau zu verfolgen.

   Hier finden Sie eine Beispielinitialisierung für `ADBMediaHeartbeatConfig`:

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Diese Instanz wird für alle der folgenden-Tracking-Ereignisse verwendet.

## Migration von Version 1.x auf 2.x in iOS {#migrate-to-two-x}

In Version 2.x sind alle öffentlichen Methoden in der Klasse `ADBMediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern. Alle Konfigurationen wurden in der Klasse `ADBMediaHeartbeatConfig` zusammengefasst.

Weitere Informationen zur Migration von 1.x zu 2.x finden Sie unter [Migration von VHL 1.x zu 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Native App für tvOS konfigurieren

Mit der neuen Apple TV-Version können Sie Anwendungen erstellen, die in der nativen tvOS-Umgebung ausgeführt werden. Sie können entweder eine rein native App mit verschiedenen in iOS verfügbaren Frameworks erstellen oder eine App über XML-Vorlagen und JavaScript erstellen. Ab MediaSDK-Version 2.0 wird tvOS unterstützt. Weitere Informationen zu tvOS finden Sie auf der [tvOS-Entwickler-Site.](https://developer.apple.com/tvos/)

Führen Sie die folgenden Schritte in Ihrem Xcode-Projekt aus. In dieser Anleitung wird davon ausgegangen, dass das Projekt eine Apple TV-App zum Ziel hat, die auf tvOS ausgerichtet ist:

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. Erweitern Sie im Tab **[!UICONTROL Build-Phasen]** des Ziels Ihrer tvOS-App den Bereich **[!UICONTROL Binär mit Bibliotheken verknüpfen]** und fügen Sie die folgenden Bibliotheken hinzu:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

