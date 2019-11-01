---
title: Wiederaufnehmen von inaktiven Sitzungen
description: Vorgehensweise zum Wiederaufnehmen einer inaktiven Sitzung.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Wiederaufnahme von inaktiven Sitzungen{#resuming-inactive-sessions}

## Lange Pausen

Das Media SDK verfolgt automatisch, wie lange die Medienwiedergabe in einem der folgenden inaktiven Status erfolgt:

* angehalten
* Suche
* Unterbrochen
* Puffern

Wenn eine Medienverfolgungssitzung länger als 30 Minuten inaktiv bleibt, wird die Sitzung automatisch geschlossen. Wenn der Anwender eine zuvor inaktive Tracking-Sitzung wiederaufnimmt (`trackPlay`), erstellt Media Heartbeat automatisch eine neue Videositzung mit den zuvor verwendeten Videoinformationen und Metadaten und sendet ein Heartbeat-Ereignis zur Wiederaufnahme. Weitere Informationen finden Sie unter [Audio- und Videoparameter.](/help/metrics-and-metadata/audio-video-parameters.md)

## Manuelles Wiederaufnehmen einer zuvor geschlossenen Sitzung

Das Media SDK nimmt Sitzungen nur dann automatisch wieder auf, wenn die Anwendung nicht geschlossen wurde. Wenn die Anwendung Benutzerdaten speichert und in der Lage ist, einen zuvor geschlossenen Datenträger wiederaufzunehmen, kann ein Wiederaufnahmeereignis manuell ausgelöst werden. Wenn Sie die Video-Tracking-Sitzung starten, legen Sie die optionale Eigenschaft zur Videowiederaufnahme fest.

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

