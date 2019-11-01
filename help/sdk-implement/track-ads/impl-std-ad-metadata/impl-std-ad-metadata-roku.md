---
title: Standard-Anzeigenmetadaten in Roku implementieren
description: Verwendung von Standard-Anzeigenmetadaten bei der Anzeigenverfolgung auf Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standard-Anzeigenmetadaten in Roku implementieren{#implement-standard-ad-metadata-on-roku}

## Implementieren von Standard-Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch mit Schlüssel/Wert-Paaren für Standard-Anzeigenmetadaten anhand der Schlüssel für Ihre Plattform:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

