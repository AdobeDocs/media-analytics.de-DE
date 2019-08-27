---
seo-title: Übersicht einrichten
title: Übersicht einrichten
uuid: 06 fefedb-b 0 c 8-4 f 7 d -90 c 8-e 374 cdde 1695
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Übersicht einrichten{#setup-overview}

>[!IMPORTANT]
>
>Die folgenden Anweisungen gelten für die 2. x Media sdks. Wenn Sie eine 1.x-Version des Medien-SDK implementieren, lesen Sie die Dokumentation zum [Medien-SDK 1.x.](/help/sdk-implement/download-sdks.md) Weitere Informationen zu Primetime Integrators finden Sie unten in _der Primetime-Media SDK-Dokumentation_ .


## Mindestunterstützung für Plattformversionen {#minimum-platform-version}

Die folgende Tabelle beschreibt die für jedes SDK unterstützten Plattformversionen, ab dem 19. Februar 2019.

| OS/Browser | Min. Version erforderlich |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0 + - Lollipop |
| Chrome | v 22 + |
| Mozilla | v 27 + |
| Safari | v 7 + |
| IE | v 11 + |

## Allgemeine Implementierungsrichtlinien {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

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

1. Implementieren Sie die `MediaHeartbeatDelegate`.

   |  Name der Methode  |  Beschreibung  | erforderlich |
   | --- | --- | :---: |
   | `getQoSObject()` | Gibt die `MediaObject`-Instanz zurück, die die aktuellen Informationen zur Servicequalität enthält. Diese Methode wird mehrmals während einer Wiedergabesitzung aufgerufen. Die Player-Implementierung muss stets die aktuellsten verfügbaren Servicequalitätsdaten zurückgeben. | Ja |
   | `getCurrentPlaybackTime()` | Gibt die aktuelle Position der Abspielleiste zurück. Bei VOD-Tracking wird der Wert in Sekunden ab Beginn des Medienelements angegeben. Beim Tracking von linearen oder Live-Assets wird der Wert in Sekunden ab Beginn des Programms angegeben. | Ja |

   >[!TIP]
   >
   >Das Servicequalitätsobjekt (Servicequalität) ist optional. Wenn QoS-Daten für Ihren Player verfügbar sind und Sie diese Daten verfolgen möchten, sind die folgenden Variablen erforderlich:

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
   >`MediaHeartbeat` erfordert eine Instanz `AppMeasurement` von Aufrufen an Adobe Analytics.

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

## Überprüfen {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

Die Implementierungen von Media Analytics-Verfolgung generieren zwei Arten von Tracking-Aufrufen:

* Medien- und Anzeigenstartanrufe werden direkt an den Adobe Analytics-Server (appmeasurement) gesendet.
* Heartbeat-Aufrufe werden an den Media Analytics-Tracking-Server (Heartbeats) gesendet, dort verarbeitet und an den Adobe Analytics-Server weitergegeben.

* **Adobe Analytics (appmeasurement)-Server**
Weitere Informationen zu den Tracking-Serveroptionen finden Sie unter [Korrektes Füllen der Variablen trackingserver und trackingserversecure.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Für den Experience Cloud Besucher-ID-Dienst ist ein RDC-Tracking-Server oder eine CNAME-Auflösung auf einem RDC-Server erforderlich.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** Media Analytics (Heartbeats) server**
Dies hat immer das Format "`[your_namespace].hb.omtrdc.net`. Der Wert von "`[your_namespace]`specifies your company" und wird von Adobe bereitgestellt.

Das Medien-Tracking verhält sich auf allen Plattformen – Desktop oder Mobilgeräte – gleich. Die Audioverfolgung funktioniert derzeit auf mobilen Plattformen. Es gibt einige universelle Variablen, die für alle Tracking-Aufrufe überprüft werden müssen:

## Dokumentation zu SDK 1. x {#section_acj_tkk_t2b}

| Video Analytics 1. x sdks  | Entwicklerhandbücher (nur pdfs) |
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
