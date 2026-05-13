---
title: Kampagnen-ID
description: Gibt die Kampagne an, zu der jede Anzeige gehört.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# Kampagnen-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting-Dimension **Kampagnen**ID) behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/ads/campaign-id.md) unter „Kampagnen-ID“*

>[!ENDSHADEBOX]

Die **Kampagnen-ID**-Dimension zeigt die Anzeigenkampagne an, zu der jede kreative Anzeige gehört. Verwenden Sie die Dimension, um die Interaktion mehrerer Kreativen zusammenzufassen, die eine Kampagne gemeinsam nutzen.

## So wird diese Dimension ausgefüllt

Die Kampagnen-ID wird vom Player bei jedem `media.adStart` Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.campaign`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videocampaign, post_videocampaign` |

## Dimensionselemente

Jedes Element ist der literale Kampagnenwert, der für `media.adStart` gemeldet wird.
