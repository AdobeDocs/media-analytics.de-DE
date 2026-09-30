---
title: Site-ID
description: Gibt für jede Anzeige die Kennung der Anzeigenseite aus.
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
source-wordcount: '150'
ht-degree: 10%
---

# Site-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Site-ID**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/site-id.md) unter „Site-ID“*

>[!ENDSHADEBOX]

Die Dimension **Site-ID** zeigt die ID der Anzeigenwebsite an (normalerweise eine ID aus Ihrer Anzeigenserverplattform). Verwenden Sie die Dimension, um die Interaktion nach Anzeigenplatzierungs-Site aufzuheben.

## So wird diese Dimension ausgefüllt

Die Site-ID wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.site` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.site` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## Dimensionselemente

Jedes Element ist der literale Site-ID-Wert, der beim Anzeigen-Start [&#x200B; wird](/help/implementation/events/ads/ad-start.md).
