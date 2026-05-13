---
title: Advertiser
description: Gibt das Unternehmen oder die Marke an, das bzw. die in jeder Anzeige zu sehen ist.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 11%

---


# Advertiser

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting **Dimension**&#x200B;Advertiser) behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/advertiser.md) unter „Advertiser“*

>[!ENDSHADEBOX]

Die Dimension **Advertiser** zeigt das Unternehmen oder die Marke an, die in jeder Anzeige enthalten ist (z. B. `"Ford"` oder `"Coca-Cola"`). Verwenden Sie die Dimension, um die Interaktion und den Abschluss durch den Advertiser auszuschalten.

## So wird diese Dimension ausgefüllt

Advertiser wird vom Player bei jedem `media.adStart` Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.advertiser`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadvertiser, post_videoadvertiser` |

## Dimensionselemente

Jedes Element ist der wörtliche Advertiser-Name, der für `media.adStart` gemeldet wird.
