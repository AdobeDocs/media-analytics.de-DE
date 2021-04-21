---
title: Standard-Metadaten in Android implementieren
description: Beschreibt das Festlegen von Standard-Video- und Anzeigenmetadaten, die mit Tracking-Aufrufen in Android gesendet werden.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '101'
ht-degree: 100%

---

# Standard-Metadaten in Android implementieren {#implement-standard-metadata-on-android}

## Standardmetadaten-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Konstante für das Anhängen von Standard-Metadaten an `MediaObject`. |

## API-Referenz für Metadatenschlüssel

* Erstellen Sie eine `HashMap` mit Schlüssel-Wert-Paaren für Standard-Metadaten.
   * [Schlüssel für Video-Metadaten](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Schlüssel für Audio-Metadaten](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Legen Sie die `HashMap` für Standard-Metadaten bei `MediaInfo` mit der Standard-Metadatenkonstante fest.
* Geben Sie dieses `MediaInfo`-Objekt an, während Sie die `trackSessionStart()`-API aufrufen.

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
