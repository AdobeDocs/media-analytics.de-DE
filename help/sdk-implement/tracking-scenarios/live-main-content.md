---
seo-title: Live-Hauptinhalt
title: Live-Hauptinhalt
uuid: e 92 e 99 f 4-c 395-48 aa -8 a 30-cbdd 2 f 5 fc 07 c
translation-type: tm+mt
source-git-commit: 9dbd621e10ba198b9331e5a7579fcbd3b6173ecd

---


# Live-Hauptinhalt{#live-main-content}

## Szenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}

In diesem Szenario gibt es ein Live-Asset ohne Wiedergabe von Anzeigen für 40 Sekunden nach Beitritt zum Live-Stream.

| Auslöser | Heartbeat-Methode | Netzwerkaufrufe | Hinweise   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics Content Start, Heartbeat Content Start | Dies kann ein Anwender sein, der auf **[!UICONTROL Abspielen]klickt, oder ein Ereignis bei automatischer Wiedergabe.** |
| Das erste Bild des Mediums wird wiedergegeben. | `trackPlay` | Heartbeat Content Play | Diese Methode löst den Timer aus. Heartbeats werden während der Dauer der Wiedergabe alle zehn Sekunden gesendet. |
| Der Inhalt wird wiedergegeben. |  | Content Heartbeats |  |
| Die Sitzung ist beendet. | `trackSessionEnd` |  | `SessionEnd` steht für das Ende einer Anzeigesitzung. Diese API muss auch dann aufgerufen werden, wenn der Benutzer die Medien nicht bis zum Ende nutzt. |

## Parameter {#section_D52B325B99DA42108EF560873907E02C}

Viele der Werte bei Adobe Analytics Content Start-Aufrufen sind auch bei Heartbeat Content Start-Aufrufen vorhanden. Außerdem werden Ihnen viele weitere Parameter angezeigt, die Adobe verwendet, um die verschiedenen Medienberichte in Adobe Analytics zu füllen. Davon werden im Folgenden nur die wichtigsten Parameter behandelt.

### Heartbeat Content Start

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe-Report Suite-ID&gt; |  |
| `s:sc:tracking_serve` | &lt;Analytics-Tracking-Server-URL&gt; |  |
| `s:user:mid` | `s:user:mid` | Sollte mit dem mid-Wert beim Adobe Analytics Content Start-Aufruf übereinstimmen |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt; Ihr Medienname &gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | optional | Benutzerspezifischer Metadatensatz, der auf den Medien eingestellt ist |

## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

Während der Medienwiedergabe gibt es einen Timer, der alle zehn Sekunden Heartbeats sendet. Diese Heartbeats enthalten Informationen zu Wiedergabe, Anzeigen, Pufferung und vielen weiteren Aspekten. Der genaue Inhalt jedes Heartbeats wird in diesem Dokument nicht behandelt. Wichtig ist vor allem, sicherzustellen, dass Heartbeats konsistent ausgelöst werden, während die Wiedergabe läuft.

Suchen Sie in den Inhalts-Heartbeats nach einigen speziellen Elementen:

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;Position der Abspielleiste&gt;, z. B. 50, 60, 70 | Dies sollte die aktuelle Position der Abspielleiste widerspiegeln. |

## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

In diesem Szenario wird kein complete-Aufruf durchgeführt, da der Live-Stream nie abgeschlossen wurde.

## Abspielkopfzeileneinstellungen

Bei LIVE-Streams müssen Sie die Abspielleiste auf einen Offset festlegen, von dem aus die Programmierung begann, damit Analysten bei der Berichterstellung bestimmen können, an welchem Punkt Benutzer beitreten und den LIVE-Stream innerhalb einer 24-Stunden-Ansicht verlassen.

### Beim Start

For LIVE media, when a user starts playing the stream, you need to set `l:event:playhead` to the current offset, in seconds. Dies ist im Gegensatz zu VOD, bei dem Sie die Abspielleiste auf "0" setzen würden.

For example, say a LIVE streaming event starts at midnight and runs for 24 hours (`a.media.length=86400`; `l:asset:length=86400`). Angenommen, ein Benutzer beginnt mit dem Live-Stream um 12:00 Uhr. In this scenario, you should set `l:event:playhead` to 43200 (12 hours into the stream).

### Anhalten

Die gleiche "Live Playhead" -Logik, die am Anfang der Wiedergabe angewendet wird, muss angewendet werden, wenn ein Benutzer die Wiedergabe hält. When the user returns to playing the LIVE stream, you must set the `l:event:playhead` value to the new offset playhead position, _not_ to the point where the user paused the LIVE stream.

## Beispielcode {#section_vct_j2j_x2b}

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

