---
description: 'null '
seo-description: 'null '
seo-title: Standard-Metadaten in Android implementieren
title: Standard-Metadaten in Android implementieren
uuid: c 48 b 4190-b 062-4 c 4 e -9 c 40-8 dde 4598 a 50 e
translation-type: tm+mt
source-git-commit: 46797deb402fed1c4d4781507c279407f8c13f2e

---


# Standard-Metadaten in Android implementieren{#implement-standard-metadata-on-android}

## Standardmetadaten-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Konstante für das Anhängen von Standard-Metadaten an `MediaObject`. |

## API-Referenz zu Metadatenschlüssel

* Create a `HashMap` of standard metadata key value pairs.
   * [Schlüssel für Videometadaten](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Schlüssel für Audio-Metadaten](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Legen Sie die `HashMap` für Standard-Metadaten bei `MediaInfo` mit der Standard-Metadatenkonstante fest.
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

## Beispielimplementierungen

### Video

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Audio

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
