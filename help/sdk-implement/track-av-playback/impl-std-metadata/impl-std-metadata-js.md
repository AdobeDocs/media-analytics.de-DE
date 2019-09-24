---
description: 'null'
seo-description: 'null'
seo-title: Standard-Metadaten in JavaScript implementieren
title: Standard-Metadaten in JavaScript implementieren
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Standard-Metadaten in JavaScript implementieren{#implement-standard-metadata-on-javascript}

## Metadatenkonstante

| Konstantenname | Beschreibung   |
| --- | --- |
| `StandardMediaMetadata` | Konstante für das Anhängen von Standard-Metadaten an `MediaObject` |

## Implementierung

Instanziieren Sie ein Standard-Metadatenobjekt, füllen Sie die gewünschten Variablen aus und setzen Sie das Metadatenobjekt auf das Media Heartbeat-Objekt. Beispiel:

```js
_onVideoLoad = function () { 
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>, 
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>); 
 
    //Set standard Video Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
 
    //Set standard Audio Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label"; 
 
    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata); 
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
}; 
```

