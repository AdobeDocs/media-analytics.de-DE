---
title: Erfahren Sie, wie Sie Standard-Metadaten in iOS implementieren.
description: Informieren Sie sich über das Festlegen von Standard-Video- und Anzeigenmetadaten, die mit Tracking-Aufrufen in iOS gesendet werden.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 100%

---

# Standard-Metadaten in iOS implementieren{#implement-standard-metadata-on-ios}

## Metadaten-Konstanten

| Konstantenname | Beschreibung   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Konstante für das Anhängen von Standard-Metadaten an `MediaInfo ADBMediaObject` |

## Implementierung

1. Erstellen Sie mit `ADBStandardMetadataKeys` ein Wörterbuch mit Schlüssel-Wert-Paaren für Standard-Metadaten.
   [iOS-Metadatenschlüssel](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Legen Sie das Wörterbuch für Standard-Metadaten bei der `MediaInfo` `ADBMediaObject`-Instanz mit der Standard-Metadatenkonstante fest.

1. Geben Sie dieses `MediaInfo`-Objekt an, während Sie die `trackSessionStart`-API aufrufen.

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
