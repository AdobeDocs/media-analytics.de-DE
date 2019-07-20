---
description: 'null '
seo-description: 'null '
seo-title: Standard-Anzeigenmetadaten in JavaScript implementieren
title: Standard-Anzeigenmetadaten in JavaScript implementieren
uuid: 4 ea 10 c 5 a-ae 2 b -45 d 0-aad 3-9 f 10028 ee 7 c 3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Standard-Anzeigenmetadaten in JavaScript implementieren{#implement-standard-ad-metadata-on-javascript}

## Anzeigenkonstanten

| Konstantenname | Beschreibung   |
|---|---|
| `StandardAdMetadata` | Konstante für das Anhängen von Standard-Anzeigenmetadaten an das Anzeigenobjekt |

## Implementierung standardmäßiger Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch mit Schlüssel/Wert-Paaren für Standard-Anzeigenmetadaten mithilfe der Schlüssel für Ihre Plattform:

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>); 
   
// Set standard Ad Metadata 
var standardAdMetadata = {}; 
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser"; 
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign"; 
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```

