---
title: Implementieren von älteren Media SDKs – Erklärung
description: Erfahren Sie, wie Sie das **ältere** Media SDK der Version 2.x für das Medien-Tracking in Ihren mobilen, OTT- und Browser-Programmen (JS) einrichten.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 99%

---

# Übersicht über die Einrichtung älterer Streaming Media SDKs der Version 2.x{#setup-overview}

Die Anweisungen in diesem Abschnitt gelten für die **älteren** Media SDKs der Version 2.x.

* Wenn Sie Version 1.x des Media SDK implementieren, lesen Sie dazu bitte die [Dokumentation zum Media SDK 1.x](/help/getting-started/download-sdks.md).

* Primetime-Integratoren lesen bitte die _Primetime-Dokumentation für Media SDKs_.

>[!IMPORTANT]
>
>Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein.  Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/additional-resources/end-of-support-faqs.md).


## Unterstützte Mindestplattformversionen {#minimum-platform-version}

In der folgenden Tabelle werden die für jedes SDK ab dem 19. Februar 2019 unterstützten Mindestplattformversionen beschrieben.

| OS/Browser | Erforderliche Mindestversion |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Allgemeine Implementierungsrichtlinien {#general-implementation-guidelines}

Das Medien-Tracking umfasst drei grundlegende SDK-Komponenten:
* Media Heartbeat Config - Die Konfiguration enthält die Grundeinstellungen für Berichte.
* Media Heartbeat Delegate - Der Delegate steuert die Wiedergabedauer und das QoS-Objekt.
* Media Heartbeat - Die primäre Bibliothek, die Elemente und Methoden enthält.

Führen Sie die folgenden Implementierungsschritte aus:

1. Erstellen Sie eine `MediaHeartbeatConfig`-Instanz und legen Sie Ihre Konfigurationsparameterwerte fest.

   |  Variablenname  | Beschreibung  | erforderlich |  Standardwert  |
   |---|---|:---:|---|
   | `trackingServer` | Tracking-Server für Medienanalyse. Dies unterscheidet sich von Ihrem Analytics-Tracking-Server. | Ja | Leere Zeichenfolge |
   | `channel` | Kanalname | Nein | Leere Zeichenfolge |
   | `ovp` | Name der Online-Medienplattform, über die der Inhalt verteilt wird. | Nein | Leere Zeichenfolge |
   | `appVersion` | Version der Medienplayer-App bzw. des SDK | Nein | Leere Zeichenfolge |
   | `playerName` | Name des verwendeten Medienplayers, d. h. „AVPlayer“, „HTML5-Player“, „Mein benutzerspezifischer Player“. | Nein | Leere Zeichenfolge |
   | `ssl` | Gibt an, ob HTTPS-Aufrufe durchgeführt werden sollen | Nein | false |
   | `debugLogging` | Gibt an, ob die Debug-Protokollierung aktiviert ist | Nein | false |

1. Implementieren des `MediaHeartbeatDelegate`.

   |  Name der Methode  |  Beschreibung  | erforderlich |
   | --- | --- | :---: |
   | `getQoSObject()` | Gibt die `MediaObject`-Instanz zurück, die die aktuellen Informationen zur Servicequalität enthält. Diese Methode wird mehrmals während einer Wiedergabesitzung aufgerufen. Die Player-Implementierung muss stets die aktuellsten verfügbaren Servicequalitätsdaten zurückgeben. | Ja |
   | `getCurrentPlaybackTime()` | Gibt die aktuelle Position der Abspielleiste zurück. <br /> Bei VOD-Tracking wird der Wert in Sekunden ab Beginn des Medienelements angegeben. <br /> Wenn der Player beim Livestreaming keine Informationen zur Inhaltsdauer bereitstellt, kann der Wert als Anzahl der Sekunden seit Mitternacht (UTC) des Tages angegeben werden. <br /> Hinweis: Bei Verwendung von Fortschrittsmarken ist die Inhaltsdauer erforderlich und der Abspielkopf muss als Anzahl von Sekunden ab Beginn des Medienelements aktualisiert werden, beginnend mit 0. | Ja |

   >[!TIP]
   >
   >Das Quality-of-Service (QoS)-Objekt ist optional. Wenn QoS-Daten für Ihren Player verfügbar sind und Sie diese Daten tracken möchten, sind die folgenden Variablen erforderlich:

   | Variablenname | Beschreibung   | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Die Bitrate von Medien in Bits pro Sekunde. | Ja |
   | `startupTime` | Die Zeitdauer bis zum Beginn von Medien in Millisekunden. | Ja |
   | `fps` | Die pro Sekunde angezeigten Frames. | Ja |
   | `droppedFrames` | Die Anzahl der bisherigen Dropped Frames. | Ja |

1. Erstellen Sie die `MediaHeartbeat`-Instanz.

   Verwenden Sie `MediaHertbeatConfig` und `MediaHertbeatDelegate`, um die `MediaHeartbeat`-Instanz zu erstellen.

   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass die `MediaHeartbeat`-Instanz zugänglich ist und ihre Zuweisung nicht vor Ende der Sitzung aufgehoben wird. Diese Instanz wird für alle der folgenden Medien-Tracking-Ereignisse verwendet.

   >[!TIP]
   >
   >`MediaHeartbeat` erfordert eine `AppMeasurement`-Instanz, um Aufrufe an Adobe Analytics senden zu können.

1. Kombinieren Sie alle Teile.

   Der folgende Beispielcode nutzt unser JavaScript 2.x-SDK für einen HTML5-Videoplayer:

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

Media Analytics-Tracking-Implementierungen generieren zwei Arten von Tracking-Aufrufen:

* Medien- und Anzeigenstartaufrufe werden direkt an den Adobe Analytics-Server (AppMeasurement) gesendet.
* Heartbeat-Aufrufe werden an den Media Analytics-Tracking-Server (Heartbeats) gesendet, dort verarbeitet und an den Adobe Analytics-Server weitergeleitet.

* **Adobe Analytics-Server (AppMeasurement)** Weitere Informationen zu den Optionen für Tracking-Server finden Sie unter [Korrektes Ausfüllen der Variablen trackingServer und trackingServerSecure.](https://helpx.adobe.com/de/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >Für den Experience Cloud Visitor ID-Dienst ist ein RDC-Tracking-Server oder CNAME erforderlich, der in einen RDC-Server aufgelöst wird.

  Der Analytics-Tracking-Server sollte auf „`.sc.omtrdc.net`“ enden oder ein CNAME sein.

* **&#x200B; Media Analytics-Server (Heartbeats)**
Dieser hat immer das Format „`[your_namespace].hb.omtrdc.net`“. Der Wert „`[your_namespace]`“gibt Ihr Unternehmen an und wird von Adobe bereitgestellt.

Das Medien-Tracking verhält sich auf allen Plattformen – Desktop oder Mobilgeräte – gleich. Das Audio-Tracking funktioniert derzeit auf mobilen Plattformen. Es gibt einige universelle Variablen, die für alle Tracking-Aufrufe überprüft werden müssen:

## Dokumentation zum SDK 1.x {#sdk-1x-documentation}

| Video Analytics-SDKs 1.x  |  Entwicklerhandbücher (nur PDFs) |
| --- | --- |
| Android | [Android-Konfiguration](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Konfigurieren von für Apple TV](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Chromecast-Konfiguration](chromecast_1.x_sdk.pdf) |
| iOS | [iOS-Konfiguration](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [JavaScript-Konfiguration](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android: [Media Analytics-Konfiguration](https://helpx.adobe.com/de/support/primetime.html) </li> <li> DHLS: [Media Analytics-Konfiguration](https://helpx.adobe.com/de/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS: [Media Analytics-Konfiguration](https://helpx.adobe.com/de/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [TVML-Konfiguration](vhl_tvml.pdf) |

## Primetime Medien-SDK-Dokumentation {#primetime-docs}

* [Primetime-Benutzerhandbücher](https://helpx.adobe.com/de/support/primetime.html)
