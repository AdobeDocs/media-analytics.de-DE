---
title: Standard-Anzeigenmetadaten in iOS implementieren
description: Verwendung von Standard-Anzeigenmetadaten beim Anzeigen-Tracking in iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standard-Anzeigenmetadaten in iOS implementieren {#implement-standard-ad-metadata-on-ios}

## Anzeigenkonstanten

| Konstantenname | Beschreibung   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Konstante für das Anhängen von Standard-Anzeigenmetadaten an `AdInfo ADBMediaObject` |

## Implementieren der Standard-Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch der Schlüssel-Werte-Paare für Standard-Anzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS-Metadataschlüssel](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
