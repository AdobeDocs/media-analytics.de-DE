---
title: VOD-Wiedergabe mit Pufferung
description: Ein Beispiel für das Tracking von VOD-Inhalten mit dem Media SDK.
uuid: 958f7692-7193-40fb-a8e7-2ff4fa805330
exl-id: 3a8f913f-cb51-45ae-ac1d-862ea1e7c994
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '228'
ht-degree: 100%

---

# VOD-Wiedergabe mit Pufferung {#vod-playback-with-buffering}

## Szenario {#scenario}

In diesem Szenario tritt Pufferung bei der Wiedergabe des VOD-Inhalts auf.

Wenn nichts anderes angegeben ist, sind die Netzwerkaufrufe in diesem Szenario mit den Aufrufen im Szenario [VOD-Wiedergabe ohne Anzeigen](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) identisch.

| Auslöser   | Heartbeat-Methode   | Netzwerkaufrufe   | Hinweise   |
|---|---|---|---|
| Anwender klickt auf **[!UICONTROL Abspielen]** | `trackSessionStart` | Analytics Content Start, Heartbeat Content Start | Dies kann ein Anwender sein, der auf **[!UICONTROL Abspielen]** klickt, oder ein Ereignis bei automatischer Wiedergabe. |
| Das erste Videobild wird wiedergegeben. | `trackPlay` | Heartbeat Content Play | Diese Methode löst den Timer aus. Heartbeats werden alle 10 Sekunden gesendet, solange die Wiedergabe läuft. |
| Der Inhalt wird wiedergegeben. |  | Content Heartbeats |  |
| Die Pufferung wird gestartet. | `trackEvent:BufferStart` | Heartbeat Buffer |  |
| Der Inhalt wird gepuffert. |  | Content Heartbeats |  |
| Die Pufferung ist abgeschlossen. | `trackEvent:BufferComplete` | Heartbeat Buffer, Heartbeat Play |  |
| Der Inhalt wird wiedergegeben. |  | Content Heartbeats |  |
| Die Inhaltswiedergabe ist abgeschlossen. | `trackComplete` | Heartbeat Content Complete | Das Ende der Abspielleiste wurde erreicht. |
| Die Sitzung ist beendet. | `trackSessionEnd` |  | `SessionEnd` steht für das Ende einer Anzeigesitzung. Diese API muss auch dann aufgerufen werden, wenn der Anwender das Video nicht bis zum Ende anschaut. |

## Parameter {#parameters}

### Heartbeat Buffer

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:event:type` | `"buffer"` |  |

## Beispielcode {#sample-code}

In diesem Szenario tritt Pufferung bei der Wiedergabe des VOD-Inhalts auf.

![](assets/buffer-regular-content.png)

### Android

Um dieses Szenario in Android anzuzeigen, verwenden Sie folgenden Code:

```java
// Set up mediaObject 

MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track the MediaHeartbeat.Event.BufferStart event when the video player  
//    goes into the buffering state and begins to buffer content. 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.BufferComplete event when the video player  
//    goes into the buffering state and begins to buffer content. 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete, null, null); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e., when the 
//    video completes and finishes playing. 
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
_mediaHeartbeat.trackSessionEnd(); 

........ 
```

### iOS

Um dieses Szenario in iOS anzuzeigen, verwenden Sie folgenden Code:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 
 
NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
....... 
....... 

// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay];  
....... 
....... 

// 3. Track the trackEvent:ADBMediaHeartbeatEventBufferStart event when the  
//    video player goes in buffering state and begins to buffer content. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 4. Track the trackEvent:ADBMediaHeartbeatEventBufferComplete event when  
//    the video player goes in buffering state and begins to buffer content. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 5. Call trackComplete when the playback reaches the end, i.e., when the 
//    video completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 6. Call trackSessionEnd when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

### JavaScript

Geben Sie den folgenden Text ein, um dieses Szenario anzuzeigen:

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

var videoMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of the ad video is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track event MediaHeartbeat.Event.BufferStart when the video player  
//    goes into the buffering state and begins to buffer content. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.BufferComplete event when the  
//    video player goes into the buffering state and begins to buffer content. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e.,  
//    when playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```
