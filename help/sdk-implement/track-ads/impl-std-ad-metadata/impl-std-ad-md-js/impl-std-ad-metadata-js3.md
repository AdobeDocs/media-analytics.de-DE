---
title: Implementieren von Standard-Anzeigenmetadaten mit JavaScript 3.x
description: Verwendung von Standard-Anzeigenmetadaten beim Tracking von Anzeigen in einem Browser mit JavaScript 3.x-Programmen.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '54'
ht-degree: 100%

---

# Implementieren von Standard-Anzeigenmetadaten mit JavaScript 3.x {#implement-standard-ad-metadata-on-javascript}

## Implementieren der Standard-Anzeigenmetadaten

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch der Schlüssel-Werte-Paare für Standard-Anzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform:

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
