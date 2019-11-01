---
title: Standard-Metadaten in Android implementieren
description: Beschreibt das Festlegen von Standard-Video- und Anzeigenmetadaten, die mit Verfolgungsaufrufen unter Android gesendet werden.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standard-Metadaten in Android implementieren{#implement-standard-metadata-on-android}

## Standardmetadaten-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Konstante für das Anhängen von Standard-Metadaten an `MediaObject`. |

## API-Referenz zu Metadatenschlüsseln

* Erstellen Sie eine `HashMap` Liste mit Schlüssel/Wert-Paaren für Standard-Metadaten.
   * [Schlüssel zu Videometadaten](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Audio-Metadatenschlüssel](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
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
