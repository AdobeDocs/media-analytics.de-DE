---
title: Einrichten des Media SDK unter iOS
description: Führen Sie diese Schritte aus, um die Media SDK-Anwendung unter iOS einzurichten.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 98%

---

# Einrichten von iOS{#set-up-ios}

Erfahren Sie, wie Sie Streaming Media Analytics für iOS-Geräte einrichten.

>[!IMPORTANT]
>
>Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein.  Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/sdk-implement/end-of-support-faqs.md).

## Voraussetzungen

* **Gültige Konfigurationsparameter für Media SDK festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **ADBMobile für iOS in Ihre Anwendung implementieren:** Weitere Informationen zur Adobe Mobile-SDK-Dokumentation finden Sie unter [iOS-SDK 4.x für Experience Cloud-Lösungen.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html?lang=de)

   >[!IMPORTANT]
   >
   >Mit iOS 9 hat Apple eine Funktion namens App Transport Security (ATS) eingeführt. Mit dieser Funktion soll die Netzwerksicherheit verbessert werden, indem sichergestellt wird, dass Ihre Apps nur Protokolle und Codes des Industriestandards verwenden. Diese Funktion ist standardmäßig aktiviert, Sie haben jedoch Konfigurationsoptionen, in denen Sie die Verwendung von ATS auswählen können. Weitere Informationen zu ATS finden Sie unter [App Transport Security.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html?lang=de)

* **Stellen Sie die folgenden Funktionen in Ihrem Medienplayer bereit:**

   * _Eine API zum Abonnieren von Player-Ereignissen_: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * _Eine API, die Player-Informationen bereitstellt_: Diese Informationen enthalten Details wie den Mediennamen und die Abspielposition.

## SDK-Implementierung

>[!IMPORTANT]
>
>Ab Version 2.3.0 wird das SDK über XCFrameworks verteilt.
>
>Für Version 2.3.0 des SDK ist Xcode 12.0 oder höher und, falls verwendet, Cocoapods 1.10.0 oder höher erforderlich.

* Jedes Mal, wenn eine Binärbibliotheksdatei erwähnt wird, sollte stattdessen deren XCFramework-Ersatz verwendet werden:
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xcframework
* Wenn Sie die Adobe XCFrameworks manuell zu Ihrem Projekt hinzufügen, stellen Sie sicher, dass sie nicht eingebettet sind.

1. Fügen Sie Ihr [heruntergeladenes](/help/sdk-implement/download-sdks.md#download-2x-sdks) Medien-SDK zu Ihrem Projekt hinzu.

   1. Stellen Sie sicher, dass die folgenden Softwarekomponenten im Verzeichnis `libs` vorhanden sind:

      * `ADBMediaHeartbeat.h`: Die Objective-C-Header-Datei, die für iOS Heartbeat-Tracking-APIs verwendet wird.
      * `ADBMediaHeartbeatConfig.h`: Die Objective-C-Header-Datei für die SDK-Konfiguration.
      * `MediaSDK.a`: Eine Bitcode-fähige Fat Binary, die die Bibliotheks-Builds für iOS-Geräte (armv7, armv7s, arm64) und Simulatoren (i386 und x86_64) enthält.

         Diese Binärdatei sollte verknüpft werden, wenn das Ziel für eine iOS-App vorgesehen ist.

      * `MediaSDK_TV.a`: Eine Bitcode-fähige Fat Binary, die die Bibliotheks-Builds für neue Apple TV-Geräte (arm64) und Simulatoren (x86_64) enthält.

         Diese Binärdatei sollte verknüpft werden, wenn das Ziel für eine Apple TV (tvOS)-App vorgesehen ist.
   1. Fügen Sie die Bibliothek zu Ihrem Projekt hinzu:

      1. Starten Sie die XCode IDE und öffnen Sie die App.
      1. Ziehen Sie im **[!UICONTROL Projektnavigator]** das Verzeichnis `libs` per Drag-and-drop in das Projekt.

      1. Stellen Sie sicher, dass das Kontrollkästchen **[!UICONTROL Elemente bei Bedarf kopieren]** aktiviert ist, die Option **[!UICONTROL Gruppen erstellen]** ausgewählt wurde und keines der Kontrollkästchen in **[!UICONTROL Zu Ziel hinzufügen]** aktiviert ist.

         ![](assets/choose-options_ios.png)

      1. Klicken Sie auf **[!UICONTROL Fertigstellen]**.
      1. Wählen Sie im **[!UICONTROL Projektnavigator]** Ihre App und Ziele aus.
      1. Verknüpfen Sie im Bereich **[!UICONTROL Verknüpfte Frameworks]** und **[!UICONTROL Bibliotheken]** im Tab **[!UICONTROL Allgemein]** die erforderlichen Frameworks und Bibliotheken.

         **iOS-App-Ziele:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Apple TV (tvOS)-Ziele:**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Überprüfen Sie, ob Ihre App ohne Fehler erstellt wird.




1. Importieren Sie die Bibliothek.

   ```
   #import "ADBMediaHeartbeat.h"
   #import "ADBMediaHeartbeatConfig.h"
   ```

1. Erstellen Sie eine `ADBMediaHeartbeatConfig`-Instanz.

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

1. Implementieren Sie das `ADBMediaHeartbeatDelegate`-Protokoll.

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

1. Verwenden Sie `ADBMediaHeartBeatConfig` und `ADBMediaHeartBeatDelegate`, um die `ADBMediaHeartbeat`-Instanz zu erstellen.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass die `ADBMediaHeartbeat`-Instanz zugänglich ist und ihre Zuweisung *nicht vor Ende der Sitzung aufgehoben wird*. Diese Instanz wird für alle der folgenden-Tracking-Ereignisse verwendet.

## Migration von Version 1.x auf 2.x in iOS {#migrate-to-two-x}

In Version 2.x sind alle öffentlichen Methoden in der Klasse `ADBMediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern. Alle Konfigurationen wurden in der Klasse `ADBMediaHeartbeatConfig` zusammengefasst.

Weitere Informationen zur Migration von 1.x zu 2.x finden Sie unter [Migration von VHL 1.x zu 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Native App für tvOS konfigurieren

Mit der Veröffentlichung des neuen Apple TV können Sie jetzt Anwendungen erstellen, die in der nativen tvOS-Umgebung ausgeführt werden. Sie können entweder eine rein native App mit einem der verschiedenen in iOS verfügbaren Frameworks oder eine App mit XML-Vorlagen und JavaScript erstellen. Ab MediaSDK Version 2.0 wird tvOS unterstützt. Weitere Informationen zu tvOS finden Sie auf der [tvOS-Entwickler-Site.](https://developer.apple.com/tvos/)

Führen Sie die folgenden Schritte in Ihrem Xcode-Projekt aus. Bei dieser Anleitung wird angenommen, dass Ihr Projekt als Ziel eine Apple TV-App hat, die tvOS auswählt:

1. Ziehen Sie die Bibliotheksdatei `VideoHeartbeat_TV.a` in den `lib`-Ordner Ihres Projekts.

1. Erweitern Sie im Tab **[!UICONTROL Build-Phasen]** des Ziels Ihrer tvOS-App den Bereich **[!UICONTROL Binär mit Bibliotheken verknüpfen]** und fügen Sie die folgenden Bibliotheken hinzu:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
