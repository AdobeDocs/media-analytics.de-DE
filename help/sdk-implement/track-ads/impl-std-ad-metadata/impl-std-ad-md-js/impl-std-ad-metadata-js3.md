---
title: Implementieren von Standard-Anzeigenmetadaten mit JavaScript 3.x
description: Verwendung von Standard-Anzeigenmetadaten bei der Anzeigenverfolgung in einem Browser mit JavaScript 3.x-Apps.
translation-type: tm+mt
source-git-commit: 83b38ac8f7fc88f982d194e776efccf8d5b983e4
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 44%

---


# Implementieren von Standard-Anzeigenmetadaten mit JavaScript 3.x{#implement-standard-ad-metadata-on-javascript}

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
