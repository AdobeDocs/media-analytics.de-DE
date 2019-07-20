---
description: 'null '
seo-description: 'null '
seo-title: Standard-Anzeigenmetadaten in Roku implementieren
title: Standard-Anzeigenmetadaten in Roku implementieren
uuid: 20 a 437 d 7-18 b 8-4099-ac 81-9 f 3628384236
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Standard-Anzeigenmetadaten in Roku implementieren{#implement-standard-ad-metadata-on-roku}

## Implementierung standardmäßiger Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch mit Schlüssel/Wert-Paaren für Standard-Anzeigenmetadaten mithilfe der Schlüssel für Ihre Plattform:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

