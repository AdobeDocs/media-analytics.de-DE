---
title: SDK-Debugging
description: Hier wird die im Media SDK verfügbare Verfolgung (Tracking)/Protokollierung beschrieben.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: ht
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a
workflow-type: ht
source-wordcount: '271'
ht-degree: 100%

---


# SDK-Debugging {#sdk-debugging}

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

## Testen von Chromecast-Anwendungen mit Adobe Bloodhound

Bei der Anwendungsentwicklung können Sie in Bloodhound die Server-Aufrufe lokal anzeigen und die Daten optional an Adobe-Erfassungs-Server weiterleiten.

<!--
For more information about Bloodhound, see the following guides:

* [Bloodhound 3.x for Mac](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwiimfSUypDpAhVZHzQIHS6WDQIQFjABegQIChAD&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound%2F&usg=AOvVaw3t4s0gcvuWEpLIqBkhKdGH) 
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)
-->

>[!IMPORTANT]
>
>Am 30. April 2017 wurde die Entwicklung von Adobe Bloodhound eingestellt. Seit dem 1. Mai 2017 wurde keine Verbesserung mehr vorgenommen und es wird kein zusätzlicher Engineering- oder Adobe Expert Care-Support mehr angeboten.

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

