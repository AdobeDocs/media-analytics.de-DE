---
title: SDK-Debugging
description: Erfahren Sie mehr über das/die im Media SDK verfügbare Tracking/Protokollierung.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 100%

---

# SDK-Debugging{#sdk-debugging}

Sie können die Protokollierung aktivieren und deaktivieren. Das Media SDK bietet einen umfassenden Tracking-/Protokollierungsmechanismus im gesamten Medien-Tracking-Stapel. Sie können diese Protokollierung aktivieren bzw. deaktivieren, indem Sie die `debugLogging`-Markierung im Config-Objekt festlegen.

## Beispielcode für die Debug-Protokollierung

### Android

```java
// Media Heartbeat initialization
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.debugLogging = true;

// Use this space for setting other config values
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config);
```

### iOS

```
// Media Heartbeat Initialization
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
config.debugLogging = YES;

// Use this space for setting other config values
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### JavaScript

```js
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.debugLogging = true;
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### OTT (Chromecast, Roku)

Die ADBMobile-Bibliothek bietet Debug-Protokollierung über die Methode `setDebugLogging`. Die Debug-Protokollierung sollte für alle Produktionsanwendungen auf `false` festgelegt werden.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Protokollmeldungen

Protokollmeldungen haben folgendes Format:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** Dies ist die aktuelle CPU-Zeit (Zeitzone GMT)
* **level:** Es sind vier Meldungsebenen definiert:
   * INFO - Normalerweise die Eingabedaten aus der Anwendung (Player-Namen, Video-ID usw. validieren)
   * DEBUG - Debug-Protokolle, die von den Entwicklern zum Debugging komplexerer Probleme verwendet werden
   * WARN - Gibt potenzielle Integrations-/Konfigurationsfehler oder Heartbeats-SDK-Fehler an
   * ERROR - Zeigt wichtige Integrationsfehler oder Heartbeats-SDK-Fehler an
* **tag:** Der Name der Unterkomponente, die die Protokollmeldung ausgegeben hat (normalerweise der Name der Klasse)
* **message:** Die tatsächliche Trace-Meldung

Sie können die Implementierung anhand der ausgegebenen Protokolle der Media SDK-Bibliothek überprüfen. Dabei bietet es sich an, in den Protokollen nach der Zeichenfolge `#track` zu suchen. Dadurch werden alle `track*()`-Aufrufe hervorgehoben, die von der Anwendung durchgeführt wurden.

Nach `#track` gefilterte Protokolle könnten beispielsweise so aussehen:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad()
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart()
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay()
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart()
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart()
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete()
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart()
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause()
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete()
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```
