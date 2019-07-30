---
description: 'null '
seo-description: 'null '
seo-title: Standard-Metadaten in iOS implementieren
title: Standard-Metadaten in iOS implementieren
uuid: 75 a 80 f 08-4 a 95-49 d 4-a 27 a -8 ce 531 d 64 d 31
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Standard-Metadaten in iOS implementieren{#implement-standard-metadata-on-ios}

## Metadaten-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Konstante für das Anhängen von Standard-Metadaten an `MediaInfo ADBMediaObject` |

## Implementierung

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys`
   [IOS-Metadatenschlüssel](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Legen Sie das Wörterbuch für Standard-Metadaten bei der `MediaInfo``ADBMediaObject` --Instanz mit der Standard-Metadatenkonstante fest.

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

### Beispielimplementierung

Instanziieren Sie ein Standard-Metadatenobjekt, füllen Sie die gewünschten Variablen aus und setzen Sie das Metadatenobjekt auf das Media Heartbeat-Objekt. Beispiel:

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

