---
title: Live-Hauptinhalt
description: Sehen Sie sich ein Beispiel für das Tracking von Live-Inhalten mit dem Media SDK an.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oOshJZEQmXqgNh5l10-qhLMO8dmph6Tz9mpH0a4FePU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 590
ht-degree: 98%

---

# Live-Hauptinhalt{#live-main-content}

## Szenario {#scenario}

In diesem Szenario gibt es ein einziges Live-Asset ohne Anzeigen, das 40 Sekunden nach Eintritt eines Benutzers in den Live-Stream wiedergegeben wird.

| Auslöser | Heartbeat-Methode | Netzwerkaufrufe | Hinweise   |
|---|---|---|---|
| Anwender klickt auf **[!UICONTROL Abspielen]** | `trackSessionStart` | Analytics Content Start, Heartbeat Content Start | Dies kann ein Anwender sein, der auf **[!UICONTROL Abspielen]** klickt, oder ein Ereignis bei automatischer Wiedergabe. |
| Das erste Medienbild wird wiedergegeben. | `trackPlay` | Heartbeat Content Play | Diese Methode löst den Timer aus. Heartbeats werden alle 10 Sekunden gesendet, solange die Wiedergabe läuft. |
| Der Inhalt wird wiedergegeben. |  | Content Heartbeats |  |
| Die Sitzung ist beendet. | `trackSessionEnd` |  | `SessionEnd` steht für das Ende einer Anzeigesitzung. Diese API muss auch dann aufgerufen werden, wenn der Benutzer die Medien nicht bis zum Ende konsumiert. |

## Parameter {#parameters}

Viele der Werte bei Adobe Analytics Content Start-Aufrufen sind auch bei Heartbeat Content Start-Aufrufen vorhanden. Außerdem verwendet Adobe noch viele weitere Parameter, um die verschiedenen Medienberichte in Adobe Analytics zu füllen. Davon werden im Folgenden nur die wichtigsten Parameter behandelt.

### Heartbeat Content Start

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe-Report Suite-ID> |  |
| `s:sc:tracking_serve` | &lt;Analytics-Tracking-Server-URL> |  |
| `s:user:mid` | `s:user:mid` | Sollte mit dem mid-Wert beim Adobe Analytics Content Start-Aufruf übereinstimmen |
| `s:event:type` | &quot;start&quot; |  |
| `s:asset:type` | &quot;main&quot; |  |
| `s:asset:mediao_id` | &lt;Ihr Medienname> |  |
| `s:stream:type` | live |  |
| `s:meta:*` | optional | Im Medium festgelegte benutzerdefinierte Metadaten |

## Content Heartbeats {#content-heartbeats}

Während der Medienwiedergabe gibt es einen Timer, der alle 10 Sekunden einen oder mehrere Heartbeats (oder Pings) für Hauptinhalte und jede Sekunde für Anzeigen sendet. Diese Heartbeats enthalten Informationen über Wiedergabe, Anzeigen, Pufferung und eine Reihe anderer Dinge. Der genaue Inhalt eines jeden Heartbeat geht über den Rahmen dieses Dokuments hinaus. Wichtig ist, dass Heartbeats laufend während der Wiedergabe ausgelöst werden.

Suchen Sie in den Content Heartbeats nach einigen spezifischen Elementen:

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:event:type` | &quot;play&quot; |  |
| `l:event:playhead` | &lt;Position der Abspielleiste>, z. B. 50, 60, 70 | Dies sollte die aktuelle Position der Abspielleiste widerspiegeln. |

## Heartbeat Content Complete {#heartbeat-content-complete}

In diesem Szenario wird kein Abschlussaufruf gesendet, da der Live-Stream nie abgeschlossen wurde.

## Einstellungen der Abspielleistenwerte

Bei LIVE-Streams müssen Sie den Wert des Abspielkopfs als die Anzahl der Sekunden seit Mitternacht UTC an diesem Tag festlegen, damit Analysten beim Reporting bestimmen können, an welchem Punkt Benutzer innerhalb einer 24-Stunden-Ansicht dem LIVE-Stream beitreten und ihn verlassen.

### Am Anfang

Bei LIVE-Medien müssen Sie, wenn ein Benutzer mit der Wiedergabe des Streams beginnt, `l:event:playhead` auf die Anzahl der Sekunden seit Mitternacht UTC an diesem Tag setzen. Dies ist anders als bei VOD, wo Sie den Abspielkopf auf „0“ festlegen würden. Hinweis: Bei Verwendung von Fortschrittsmarken ist die Inhaltsdauer erforderlich und der Abspielkopf muss als Anzahl von Sekunden ab Beginn des Medienelements aktualisiert werden, beginnend mit 0.

Beispiel: Ein LIVE-Streaming-Ereignis beginnt um Mitternacht und dauert 24 Stunden (`a.media.length=86400`; `l:asset:length=86400`). Angenommen, ein Benutzer beginnt mit der Wiedergabe dieses LIVE-Streams um 12 :00pm. In diesem Szenario sollten Sie `l:event:playhead` auf 43200 setzen (12 Stunden seit Mitternacht UTC an diesem Tag in Sekunden).

### Beim Anhalten

Dieselbe Live-Abspielleistenlogik, die zu Beginn der Wiedergabe angewendet wurde, muss angewendet werden, wenn ein Benutzer die Wiedergabe anhält. Wenn der Benutzer zum Abspielen des LIVE-Streams zurückkehrt, müssen Sie den Wert `l:event:playhead` auf die neue Anzahl der Sekunden seit Mitternacht UTC festlegen, _nicht_ auf den Punkt, an dem der Benutzer den LIVE-Stream angehalten hat.

## Beispielcode {#sample-code}

![](assets/live-content-playback.png)

### Android

Die erwartete API-Aufrufreihenfolge lautet wie folgt:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS

Die erwartete API-Aufrufreihenfolge lautet wie folgt:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

Die erwartete API-Aufrufreihenfolge lautet wie folgt:

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```
