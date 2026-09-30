---
title: Advertiser
description: Gibt das Unternehmen oder die Marke an, das bzw. die in jeder Anzeige zu sehen ist.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 13%
---

# Advertiser

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting **Dimension**&#x200B;Advertiser) behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/advertiser.md) unter „Advertiser“*

>[!ENDSHADEBOX]

Die Dimension **Advertiser** zeigt das Unternehmen oder die Marke an, die in jeder Anzeige enthalten ist (z. B. `"Ford"` oder `"Coca-Cola"`). Verwenden Sie die Dimension, um die Interaktion und den Abschluss durch den Advertiser auszuschalten.

## So wird diese Dimension ausgefüllt

Der Advertiser wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.advertiser`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## Dimensionselemente

Jedes Element ist der wörtliche Advertiser-Name, der beim [Anzeigenstart](/help/implementation/events/ads/ad-start.md) angezeigt wird.
