---
seo-title: Live-Hauptinhalt
title: Live-Hauptinhalt
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Live-Hauptinhalt{#live-main-content}

## Szenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}

In diesem Szenario gibt es ein Live-Asset ohne Wiedergabe von Anzeigen für 40 Sekunden nach Beitritt zum Live-Stream.

| Auslöser | Heartbeat-Methode | Netzwerkaufrufe | Hinweise   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics Content Start, Heartbeat Content Start | Dies kann ein Anwender sein, der auf **[!UICONTROL Abspielen]klickt, oder ein Ereignis bei automatischer Wiedergabe.** |
| Das erste Bild des Mediums wird wiedergegeben. | `trackPlay` | Heartbeat Content Play | Diese Methode löst den Timer aus. Heartbeats werden während der Dauer der Wiedergabe alle zehn Sekunden gesendet. |
| Der Inhalt wird wiedergegeben. |  | Content Heartbeats |  |
| Die Sitzung ist beendet. | `trackSessionEnd` |  | `SessionEnd` steht für das Ende einer Anzeigesitzung. Diese API muss auch dann aufgerufen werden, wenn der Benutzer die Medien nicht bis zum Abschluss verbraucht. |

## Parameter {#section_D52B325B99DA42108EF560873907E02C}

Viele der Werte bei Adobe Analytics Content Start-Aufrufen sind auch bei Heartbeat Content Start-Aufrufen vorhanden. Außerdem werden Ihnen viele weitere Parameter angezeigt, die Adobe zum Füllen der verschiedenen Medienberichte in Adobe Analytics verwendet. Davon werden im Folgenden nur die wichtigsten Parameter behandelt.

### Heartbeat Content Start

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe-Report Suite-ID&gt; |  |
| `s:sc:tracking_serve` | &lt;Analytics-Tracking-Server-URL&gt; |  |
| `s:user:mid` | `s:user:mid` | Sollte mit dem mid-Wert beim Adobe Analytics Content Start-Aufruf übereinstimmen |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;Ihr Medienname&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | optional | Benutzerdefinierte Metadaten, die auf dem Medium festgelegt wurden |

## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

Während der Medienwiedergabe gibt es einen Timer, der alle 10 Sekunden einen oder mehrere Heartbeats (oder Pings) für Hauptinhalte und jede Sekunde für Anzeigen sendet. Diese Heartbeats enthalten Informationen zu Wiedergabe, Anzeigen, Pufferung und vielen weiteren Aspekten. Der genaue Inhalt jedes Heartbeats wird in diesem Dokument nicht behandelt. Wichtig ist vor allem, sicherzustellen, dass Heartbeats konsistent ausgelöst werden, während die Wiedergabe läuft.

Suchen Sie in den Inhalts-Heartbeats nach einigen speziellen Elementen:

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;Position der Abspielleiste&gt;, z. B. 50, 60, 70 | Dies sollte die aktuelle Position der Abspielleiste widerspiegeln. |

## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

In diesem Szenario gibt es keinen vollständigen Aufruf, da der Live-Stream nie abgeschlossen wurde.

## Abspielkopfwerteinstellungen

Bei LIVE-Streams müssen Sie die Abspielleiste auf einen Offset vom Beginn der Programmierung einstellen, damit Analytiker in der Berichterstellung bestimmen können, zu welchem Zeitpunkt Benutzer den LIVE-Stream innerhalb einer 24-Stunden-Ansicht verbinden und verlassen.

### Am Anfang

Bei LIVE-Medien müssen Sie, wenn ein Benutzer mit der Wiedergabe des Streams beginnt, den aktuellen Offset in Sekunden `l:event:playhead` festlegen. Dies ist im Gegensatz zu VOD, wo Sie die Abspielleiste auf "0"setzen würden.

Beispiel: Ein LIVE-Streaming-Ereignis beginnt um Mitternacht und dauert 24 Stunden (`a.media.length=86400`; `l:asset:length=86400`). Nehmen wir an, ein Benutzer beginnt um 22.00 Uhr mit der Wiedergabe des LIVE-Streams. In diesem Szenario sollten Sie `l:event:playhead` auf 43200 (12 Stunden bis zum Stream) einstellen.

### Bei Anhalten

Bei Unterbrechung der Wiedergabe muss dieselbe Logik wie bei der Live-Abspielleiste angewendet werden. Wenn der Benutzer zum Abspielen des LIVE-Streams zurückkehrt, müssen Sie den `l:event:playhead` Wert auf die neue Position der Offset-Abspielleiste festlegen, _nicht_ auf den Punkt, an dem der Benutzer den LIVE-Stream angehalten hat.

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

