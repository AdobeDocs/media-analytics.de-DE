---
title: Standardmäßige Anzeigenmetadaten in Android implementieren
description: Verwendung von Standard-Anzeigenmetadaten beim Anzeigen-Tracking in Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standard-Anzeigenmetadaten in Android implementieren {#implement-standard-ad-metadata-on-android}

## Anzeigenkonstanten

| Konstantenname | Beschreibung   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Konstante für das Anhängen von Standard-Anzeigenmetadaten an das Anzeigen-`MediaObject`. |

## Implementieren der Standard-Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch der Schlüssel-Werte-Paare für Standard-Anzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

