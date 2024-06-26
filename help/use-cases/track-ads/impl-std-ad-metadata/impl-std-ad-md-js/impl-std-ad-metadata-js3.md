---
title: Lernen Sie, wie Sie Standard-Anzeigenmetadaten mit JavaScript 3.x implementieren
description: Verwendung von Standard-Anzeigenmetadaten beim Tracking von Anzeigen in einem Browser mit JavaScript 3.x-Programmen.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 100%

---

# Implementieren von Standard-Anzeigenmetadaten mit JavaScript 3.x {#implement-standard-ad-metadata-on-javascript}

## Standard-Anzeigenmetadaten implementieren

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
