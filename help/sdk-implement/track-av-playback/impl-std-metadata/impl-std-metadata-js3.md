---
title: Implementieren von Standard-Metadaten mit JavaScript 3.x
description: Beschreibt das Festlegen von Standard-Video- und Anzeigenmetadaten, die mit Tracking-Aufrufen in Browser-Anwendungen (JS) gesendet werden.
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# Implementieren von Standard-Metadaten mit JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementierung

Instanziieren Sie ein Kontextdatenobjekt und füllen Sie die gewünschten Standard-Metadatenvariablen aus. Beispiel:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    contextData[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    contextData[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    contextData[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    contextData[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
