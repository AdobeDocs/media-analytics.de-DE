---
title: SDK-Debugging
description: Erfahren Sie mehr über das/die im Media SDK verfügbare Tracking/Protokollierung.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/H62IoGbWZ3JPApfb-wFlt9P-oa3rD1kCzalpXEQ4Km0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 221
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
