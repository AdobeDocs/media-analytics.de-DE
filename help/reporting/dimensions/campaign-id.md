---
title: Kampagnen-ID
description: Gibt die Kampagne an, zu der jede Anzeige gehört.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 13%

---


# Kampagnen-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting-Dimension **Kampagnen**&#x200B;ID) behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/campaign-id.md) unter „Kampagnen-ID“*

>[!ENDSHADEBOX]

Die **Kampagnen-ID**-Dimension zeigt die Anzeigenkampagne an, zu der jede kreative Anzeige gehört. Verwenden Sie die Dimension, um die Interaktion mehrerer Kreativen zusammenzufassen, die eine Kampagne gemeinsam nutzen.

## So wird diese Dimension ausgefüllt

Die Kampagnen-ID wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.campaign`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## Dimensionselemente

Jedes Element ist der literale Kampagnenwert, der beim Anzeigen-Start [&#x200B; wird](/help/implementation/events/ads/ad-start.md).
