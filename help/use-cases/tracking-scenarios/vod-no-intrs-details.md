---
title: VOD-Wiedergabe ohne Anzeigen
description: Sehen Sie sich ein Beispiel für das Tracking der VOD-Wiedergabe an, das keine Werbung enthält.
uuid: ee2a1b79-2c2f-42e1-8e81-b62bbdd0d8cb
exl-id: 9e2240f0-da8d-4dcc-9d44-0f121c60d924
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 100%

---

# VOD-Wiedergabe ohne Anzeigen{#vod-playback-with-no-ads}

## Szenario {#scenario}

Dieses Szenario enthält ein einziges VOD-Asset ohne Anzeigen, das einmal von Anfang bis Ende wiedergegeben wird.

| Auslöser | Heartbeat-Methode | Netzwerkaufrufe | Hinweise   |
|---|---|---|---|
| Anwender klickt auf **[!UICONTROL Abspielen]** | `trackSessionStart` | Analytics Content Start, Heartbeat Content Start | Dies kann ein Benutzer sein, der auf „Abspielen“ klickt, oder ein Ereignis bei automatischer Wiedergabe. |
| Erstes Medienbild | `trackPlay` | Heartbeat Content Play | Diese Methode löst den Timer aus. Ab diesem Zeitpunkt werden alle 10 Sekunden Heartbeats während der Wiedergabe gesendet. |
| Inhaltswiedergaben |  | Content Heartbeats |  |
| Inhalt ist abgeschlossen. | `trackComplete` | Heartbeat Content Complete | *Complete* bedeutet, dass das Ende der Abspielleiste erreicht wurde. |

## Parameter {#parameters}

Viele der Werte bei Heartbeat Content Start-Aufrufen sind auch in Adobe Analytics `Content Start`-Aufrufen vorhanden. Adobe verwendet zahlreiche Parameter zum Füllen der verschiedenen Medienberichte. Es werden allerdings nur die wichtigsten Parameter in der folgenden Tabelle aufgelistet:

### Heartbeat Content Start

| Parameter | Wert | Hinweise   |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe-Report Suite-ID> |  |
| `s:sc:tracking_server` | &lt;Analytics-Tracking-Server-URL> |  |
| `s:user:mid` | muss festgelegt werden | Sollte mit dem mid-Wert beim `Adobe Analytics Content Start`-Aufruf übereinstimmen. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Ihr Medienname> |  |
| `s:meta:*` | optional | Benutzerdefinierte Metadaten, die für die Medien festgelegt wurden. |

## Heartbeat Content Play {#heartbeat-content-play}

Diese Parameter sollten fast genauso wie der `Heartbeat Content Start`-Aufruf aussehen, aber den Hauptunterschied im Parameter `s:event:type` aufweisen. Alle anderen Parameter sollten weiterhin vorhanden sein.

| Parameter | Wert | Hinweise   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Content Heartbeats {#content-heartbeats}

Während der Medienwiedergabe sendet ein Timer mindestens einen Heartbeat alle 10 Sekunden. Diese Heartbeats enthalten Informationen zur Wiedergabe, zu Anzeigen, zur Pufferung usw. Eine genaue Erklärung von Heartbeats würde über den Rahmen dieses Dokuments hinausgehen, aber das entscheidende Punkt ist, dass Heartbeats konsistent ausgelöst werden, während die Wiedergabe fortgesetzt wird.

Suchen Sie in den Content-Heartbeats nach den folgenden Parametern:

| Parameter | Wert | Hinweise   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;Position der Abspielleiste>, z. B. 50,60,70 | Dieser Parameter spiegelt die aktuelle Position der Abspielleiste wider. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Nach Abschluss der Wiedergabe (wenn also das Ende der Abspielleiste erreicht wird), wird ein `Heartbeat Content Complete`-Aufruf gesendet. Dieser Aufruf sieht wie andere Heartbeat-Aufrufe aus, enthält jedoch einige spezifische Parameter:

| Parameter | Wert | Hinweise   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Beispielcode {#sample-code}

In diesem Szenario ist der Inhalt 40 Sekunden lang. Er wird bis zum Ende ohne Unterbrechungen wiedergegeben.

![](assets/main-content-regular-playback.png)

### Android

```java
// Set up  mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay  
//    is used, i.e., there's an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts,  
//    i.e., the first frame of media is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when the playback session ends prior to the  
//    media completing to the finish. This method must be called when   
//    playback ends if the user does not watch the media to completion. When trackSessionEnd is used, trackComplete should not be called. 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// 4. Call trackComplete() when the playback reaches the end and   
//    completes, i.e., when the media finishes because it is played to completion. When trackComplete is used, trackSessionEnd does not need to be called.
_mediaHeartbeat.trackComplete(); 

........ 
........ 
```

### iOS

```
when the user clicks Play 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 

NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there's an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 

// 2. Call trackPlay when the playback actually starts, i.e., when the  
//    first frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end, i.e.,  
//    when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 

// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME, Configuration.MEDIA_ID,  
Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the main content starts, i.e.,  
//    the first frame of the media content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
    i.e., the media completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not  
//    watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........
```
