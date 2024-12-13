---
title: Implementieren von Media SDKs – Erklärung
description: Erfahren Sie, wie Sie die Media SDK für das Medien-Tracking in Ihren mobilen, OTT- und Browser-Anwendungen (JS) einrichten.
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 94%

---

# Legacy − Übersicht über das Einrichten von Media SDKs {#setup-overview}

Nachdem Sie das Media SDK für Ihre Video-App oder Ihren Player heruntergeladen haben, befolgen Sie die Informationen in diesem Abschnitt, um das Media SDK einzurichten und zu implementieren.


## Allgemeine Implementierungsrichtlinien {#general-implementation-guidelines}

Es gibt drei Hauptkomponenten von SDK, die beim Tracking mit der Streaming-Mediensammlung verwendet werden:
* Media Heartbeat Config: Die `MediaHeartbeatConfig`-Komponente enthält die grundlegenden Reporting-Einstellungen.
* Media Heartbeat Delegate: Die `MediaHeartbeatDelegate`-Komponente steuert die Wiedergabedauer und das QoS-Objekt.
* Media Heartbeat: Die `MediaHeartbeat`-Komponente ist die primäre Bibliothek, die Elemente und Methoden enthält.

## Implementieren des SDK für Streaming-Medien

Um das SDK für Streaming-Medien einzurichten und zu verwenden, führen Sie die folgenden Implementierungsschritte aus:

1. Erstellen Sie eine `MediaHeartbeatConfig`-Instanz und legen Sie Konfigurationsparameterwerte fest.

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

* ** Media Analytics-Server (Heartbeats)**
Dieser hat immer das Format „`[your_namespace].hb.omtrdc.net`“. Der Wert „`[your_namespace]`“gibt Ihr Unternehmen an und wird von Adobe bereitgestellt.

Das Medien-Tracking verhält sich auf allen Plattformen – Desktop oder Mobilgeräte – gleich. Das Audio-Tracking funktioniert derzeit auf mobilen Plattformen. Es gibt einige universelle Variablen, die für alle Tracking-Aufrufe überprüft werden müssen:
