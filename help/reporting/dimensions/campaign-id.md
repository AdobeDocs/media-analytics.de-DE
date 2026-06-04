---
title: Kampagnen-ID
description: Gibt die Kampagne an, zu der jede Anzeige gehört.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 13%

---


# Kampagnen-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting-Dimension **Kampagnen**ID) behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/ads/campaign-id.md) unter „Kampagnen-ID“*

>[!ENDSHADEBOX]

Die **Kampagnen-ID**-Dimension zeigt die Anzeigenkampagne an, zu der jede kreative Anzeige gehört. Verwenden Sie die Dimension, um die Interaktion mehrerer Kreativen zusammenzufassen, die eine Kampagne gemeinsam nutzen.

## So wird diese Dimension ausgefüllt

Die Kampagnen-ID wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.campaign`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## Dimensionselemente

Jedes Element ist der literale Kampagnenwert, der beim Anzeigen-Start [ wird](/help/implementation/events/ads/ad-start.md).
