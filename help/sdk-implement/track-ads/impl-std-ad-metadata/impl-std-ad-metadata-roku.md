---
title: Standard-Anzeigenmetadaten in Roku implementieren
description: Verwendung von Standard-Anzeigenmetadaten beim Anzeigen-Tracking in Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standard-Anzeigenmetadaten in Roku implementieren {#implement-standard-ad-metadata-on-roku}

## Implementieren der Standard-Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch der Schlüssel-Werte-Paare für Standard-Anzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

