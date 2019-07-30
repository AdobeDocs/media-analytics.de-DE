---
description: 'null '
seo-description: 'null '
seo-title: Standard-Anzeigenmetadaten in iOS implementieren
title: Standard-Anzeigenmetadaten in iOS implementieren
uuid: f 15 fb 727-5 a 5 b -46 c 5-bf 12-93 b 376 c 10 fd 1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Standard-Anzeigenmetadaten in iOS implementieren{#implement-standard-ad-metadata-on-ios}

## Anzeigenkonstanten

| Konstantenname | Beschreibung   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## Implementierung standardmäßiger Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch mit Schlüssel/Wert-Paaren für Standard-Anzeigenmetadaten mithilfe der Schlüssel für Ihre Plattform:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS-Metadataschlüssel](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
