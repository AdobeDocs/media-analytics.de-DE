---
seo-title: Setup-Übersicht
title: Setup-Übersicht
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Setup-Übersicht{#setup-overview}

>[!IMPORTANT]
>
>Die folgenden Anweisungen gelten für die 2.x Media SDKs. Wenn Sie eine 1.x-Version des Medien-SDK implementieren, lesen Sie die Dokumentation zum [Medien-SDK 1.x.](/help/sdk-implement/download-sdks.md) Informationen zu Primetime-Integratoren finden Sie in der unten stehenden Dokumentation zum _Primetime Media SDK_ .


## Unterstützung der Plattformversion {#minimum-platform-version}

In der folgenden Tabelle werden die Mindestplattformversionen beschrieben, die ab dem 19. Februar 2019 für jedes SDK unterstützt werden.

| OS/Browser | Min. Version erforderlich |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Allgemeine Implementierungsrichtlinien {#general-implementation-guidelines}

Es gibt drei Hauptkomponenten des SDK, die für die Medienverfolgung relevant sind:
* Media Heartbeat Config: Diese Konfiguration enthält die grundlegenden Reporting-Einstellungen.
* Media Heartbeat Delegate: Der Delegate kontrolliert die Wiedergabezeit und das QoS-Objekt.
* Media Heartbeat: Die primäre Bibliothek enthält Mitglieder und Methoden.

Führen Sie die folgenden Implementierungsschritte aus:

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  Variablenname  | Beschreibung  | erforderlich |  Standardwert  |
   |---|---|:---:|---|
   | `trackingServer` | Tracking-Server für die Medienanalyse. Dieser Server unterscheidet sich vom Analytics-Tracking-Server. | Ja | Leere Zeichenfolge |
   | `channel` | Kanalname | Nein | Leere Zeichenfolge |
   | `ovp` | Name der Online-Medienplattform, über die der Inhalt verteilt wird | Nein | Leere Zeichenfolge |
   | `appVersion` | Version der Medienplayer-App/des SDK | Nein | Leere Zeichenfolge |
   | `playerName` | Name des verwendeten Medienplayers, wie „AVPlayer“, „HTML5-Player“, „Mein anwenderspezifischer Player“. | Nein | Leere Zeichenfolge |
   | `ssl` | Gibt an, ob die Aufrufe über HTTPS erfolgen sollen | Nein | false |
   | `debugLogging` | Gibt an, ob die Debugging-Protokollierung aktiviert ist. | Nein | false |

1. Implementieren des `MediaHeartbeatDelegate`.

   |  Name der Methode  |  Beschreibung  | erforderlich |
   | --- | --- | :---: |
   | `getQoSObject()` | Gibt die `MediaObject`-Instanz zurück, die die aktuellen Informationen zur Servicequalität enthält. Diese Methode wird mehrmals während einer Wiedergabesitzung aufgerufen. Die Player-Implementierung muss stets die aktuellsten verfügbaren Servicequalitätsdaten zurückgeben. | Ja |
   | `getCurrentPlaybackTime()` | Gibt die aktuelle Position der Abspielleiste zurück. Bei VOD-Tracking wird der Wert in Sekunden ab Beginn des Medienelements angegeben. Beim Tracking von linearen oder Live-Assets wird der Wert in Sekunden ab Beginn des Programms angegeben. | Ja |

   >[!TIP]
   >
   >Das Quality of Service (QoS)-Objekt ist optional. Wenn QoS-Daten für Ihren Player verfügbar sind und Sie diese Daten verfolgen möchten, sind die folgenden Variablen erforderlich:

   | Variablenname | Beschreibung   | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Die Bitrate von Medien in Bits pro Sekunde. | Ja |
   | `startupTime` | Die Startzeit von Medien in Millisekunden. | Ja |
   | `fps` | Die pro Sekunde angezeigten Frames. | Ja |
   | `droppedFrames` | Die Anzahl der bisher abgebrochenen Bilder. | Ja |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. Diese Instanz wird für alle der folgenden Medien-Tracking-Ereignisse verwendet.

   >[!TIP]
   >
   >`MediaHeartbeat` erfordert eine Instanz von , `AppMeasurement` um Aufrufe an Adobe Analytics zu senden.

1. Kombinieren Sie die verschiedenen Elemente.

   Der folgende Beispielcode nutzt das JavaScript 2.x-SDK für einen HTML5-Videoplayer:

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Überprüfen {#validate}

Media Analytics-Verfolgungsimplementierungen generieren zwei Arten von Verfolgungsaufrufen:

* Media- und Anzeigenstartaufrufe werden direkt an den Adobe Analytics-Server (AppMeasurement) gesendet.
* Heartbeat-Aufrufe werden an den Media Analytics-Tracking-Server (Heartbeats) gesendet, dort verarbeitet und an den Adobe Analytics-Server weitergeleitet.

* **Adobe Analytics-Server (AppMeasurement)** Weitere Informationen zu den Optionen für Tracking-Server finden Sie unter [Korrektes Füllen der Variablen trackingServer und trackingServerSecure.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Für den Experience Cloud-Besucher-ID-Dienst ist ein RDC-Tracking-Server oder CNAME erforderlich, der auf einem RDC-Server aufgelöst wird.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** Media Analytics (Heartbeats) server**Dies hat immer das Format "`[your_namespace].hb.omtrdc.net`". Der Wert "`[your_namespace]`"gibt Ihr Unternehmen an und wird von Adobe bereitgestellt.

Das Medien-Tracking verhält sich auf allen Plattformen – Desktop oder Mobilgeräte – gleich. Die Audioverfolgung funktioniert derzeit auf mobilen Plattformen. Es gibt einige universelle Variablen, die für alle Tracking-Aufrufe überprüft werden müssen:

## SDK 1.x-Dokumentation {#sdk-1x-documentation}

| Video Analytics 1.x SDKs |  Entwicklerhandbücher (nur PDFs) |
| --- | --- |
| Android | [Android-Konfiguration ](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Apple TV-Konfiguration ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Chromecast-Konfiguration ](chromecast_1.x_sdk.pdf) |
| iOS | [iOS-Konfiguration ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript-Konfiguration ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML-Konfiguration ](vhl_tvml.pdf) |

## Primetime Medien-SDK-Dokumentation {#primetime-docs}

* [Primetime-Benutzerhandbücher](https://helpx.adobe.com/primetime/user-guide.html)
