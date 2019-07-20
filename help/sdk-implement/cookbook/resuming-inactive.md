---
seo-title: Wiederaufnehmen von inaktiven Sitzungen
title: Wiederaufnehmen von inaktiven Sitzungen
uuid: 3 ff 1205 d -7 bbe -4016-9 bd 7-6 e 34 b 7862 c 4 c
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Wiederaufnahme von inaktiven Sitzungen{#resuming-inactive-sessions}

## Lange Pausen

Das Media SDK verfolgt automatisch, wie lange die Medienwiedergabe in einem der folgenden inaktiven Status ist:

* angehalten
* Suche
* Unterbrochen
* Puffern

Wenn eine Medienverfolgungssitzung länger als 30 Minuten lang inaktiv bleibt, wird die Sitzung automatisch geschlossen. Wenn der Anwender eine zuvor inaktive Tracking-Sitzung wiederaufnimmt (`trackPlay`), erstellt Media Heartbeat automatisch eine neue Videositzung mit den zuvor verwendeten Videoinformationen und Metadaten und sendet ein Heartbeat-Ereignis zur Wiederaufnahme. Weitere Informationen finden Sie unter [Audio- und Videoparameter.](../../metrics-and-metadata/audio-video-parameters.md)

## Zuvor geschlossene Sitzung manuell fortsetzen

Das Media-SDK nimmt Sitzungen nur automatisch wieder auf, wenn die Anwendung nicht geschlossen wurde. Wenn die Anwendung Benutzerdaten speichert und die Möglichkeit hat, zuvor geschlossene Medien fortzusetzen, kann ein Wiederaufnahmeereignis manuell ausgelöst werden. Wenn Sie die Video-Tracking-Sitzung starten, legen Sie die optionale Eigenschaft zur Videowiederaufnahme fest.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true 
public void onmediaLoad(Observable observable, Object data) { 

  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Set to true if this is a resume playback scenario 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);
   
  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification { 
  //Replace <MEDIA_NAME> with the media name. 
  //Replace <MEDIA_ID> with a media unique identifier. 
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                       mediaId:<MEDIA_ID> 
                       length:<MEDIA_LENGTH> 
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 

  //Set to YES if this user is resuming a previously closed media session 
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata]; 
} 
```

### JavaScript

```js
_onmediaLoad = function () { 
  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session 
  mediaObject.setValue(MediaObjectKey.mediaResumed, true); 
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

