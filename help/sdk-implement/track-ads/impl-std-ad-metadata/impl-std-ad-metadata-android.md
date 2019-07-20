---
description: 'null '
seo-description: 'null '
seo-title: Standardmäßige Anzeigenmetadaten in Android implementieren
title: Standardmäßige Anzeigenmetadaten in Android implementieren
uuid: 19 b 98 bc 1-c 659-4182-a 4 ff-b 3340 fe 2453 c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Standard-Anzeigenmetadaten in Android implementieren{#implement-standard-ad-metadata-on-android}

## Anzeigenkonstanten

| Konstantenname | Beschreibung   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Konstante für das Anhängen von Standard-Anzeigenmetadaten an das Anzeigen-`MediaObject`. |

## Implementierung standardmäßiger Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch mit Schlüssel/Wert-Paaren für Standard-Anzeigenmetadaten mithilfe der Schlüssel für Ihre Plattform:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

