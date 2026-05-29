---
title: Advertiser
description: Gibt das Unternehmen oder die Marke an, das bzw. die in jeder Anzeige zu sehen ist.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.advertiser`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## Dimensionselemente

Jedes Element ist der wörtliche Advertiser-Name, der beim [Anzeigenstart](/help/implementation/events/ads/ad-start.md) angezeigt wird.
