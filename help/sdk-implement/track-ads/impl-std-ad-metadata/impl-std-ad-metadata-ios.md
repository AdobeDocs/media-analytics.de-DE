---
title: Erfahren Sie, wie Sie Standard-Anzeigenmetadaten in iOS implementieren
description: Verwendung von Standard-Anzeigenmetadaten beim Anzeigen-Tracking in iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 86%

---

# Standard-Anzeigenmetadaten in iOS implementieren{#implement-standard-ad-metadata-on-ios}

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

[iOS-Metadatenelemente](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
