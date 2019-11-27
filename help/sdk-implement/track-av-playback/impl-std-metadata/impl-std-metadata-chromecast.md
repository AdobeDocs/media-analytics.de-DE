---
title: Standard-Metadaten in Chromecast implementieren
description: Beschreibt das Festlegen von Standard-Video- und Anzeigenmetadaten in Chromecast.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standard-Metadaten in Chromecast implementieren {#implement-standard-metadata-on-chromecast}

Instanziieren Sie ein Standard-Metadatenobjekt, füllen Sie die gewünschten Variablen aus und setzen Sie das Metadatenobjekt auf das Media Heartbeat-Objekt. Beispiel:

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {}; 
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist"; 
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

Sehen Sie hier die umfassende Liste der verfügbaren Audio- und Video-Metadaten: [Audio- und Videoparameter.](/help/metrics-and-metadata/audio-video-parameters.md)
