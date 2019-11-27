---
title: Standard-Anzeigenmetadaten in JavaScript implementieren
description: Verwendung von Standard-Anzeigenmetadaten beim Anzeigen-Tracking in Browser-Anwendungen (JS).
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Standard-Anzeigenmetadaten in JavaScript implementieren {#implement-standard-ad-metadata-on-javascript}

## Anzeigenkonstanten

| Konstantenname | Beschreibung   |
|---|---|
| `StandardAdMetadata` | Konstante für das Anhängen von Standard-Anzeigenmetadaten an das Anzeigenobjekt |

## Implementieren der Standard-Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch der Schlüssel-Werte-Paare für Standard-Anzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform:

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

