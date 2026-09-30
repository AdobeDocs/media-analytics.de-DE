---
title: Platzierungs-ID
description: Gibt die Platzierungskennung für jede Anzeige an.
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
source-wordcount: '151'
ht-degree: 10%
---

# Platzierungs-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Platzierungs-ID**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/ads/placement-id.md) unter „Platzierungs-ID“*

>[!ENDSHADEBOX]

Die Dimension **Platzierungs-ID** zeigt die Anzeigenplatzierungs-ID an (normalerweise ein Slot oder eine Zone, die in Ihrer Anzeigenserver-Plattform definiert ist). Verwenden Sie die Dimension , um die Interaktion und den Abschluss über Platzierungs-Slots hinweg zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Platzierungs-ID wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.placement` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.placement` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.ad.placement` |

## Dimensionselemente

Jedes Element ist der literale Platzierungswert, der für „Anzeigenstart[ gemeldet ](/help/implementation/events/ads/ad-start.md).
