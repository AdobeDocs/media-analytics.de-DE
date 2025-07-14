---
title: Erfahren Sie, wie Sie Standard-Anzeigenmetadaten in Android implementieren.
description: Verwendung von Standard-Anzeigenmetadaten beim Anzeigen-Tracking in Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 100%

---

# Standardmäßige Anzeigenmetadaten in Android implementieren {#implement-standard-ad-metadata-on-android}

## Anzeigenkonstanten

| Konstantenname | Beschreibung   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Konstante für das Anhängen von Standard-Anzeigenmetadaten an das Anzeigen-`MediaObject`. |

## Standard-Anzeigenmetadaten implementieren

Erstellen Sie für Standard-Anzeigenmetadaten ein Wörterbuch der Schlüssel-Werte-Paare für Standard-Anzeigenmetadaten unter Verwendung der Schlüssel für Ihre Plattform:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
