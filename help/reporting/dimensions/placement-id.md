---
title: Platzierungs-ID
description: Gibt die Platzierungskennung für jede Anzeige an.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 10%

---


# Platzierungs-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Platzierungs-ID**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/placement-id.md) unter „Platzierungs-ID“*

>[!ENDSHADEBOX]

Die Dimension **Platzierungs-ID** zeigt die Anzeigenplatzierungs-ID an (normalerweise ein Slot oder eine Zone, die in Ihrer Anzeigenserver-Plattform definiert ist). Verwenden Sie die Dimension , um die Interaktion und den Abschluss über Platzierungs-Slots hinweg zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Platzierungs-ID wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.placement` einer eVar zuordnet. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.placement` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.ad.placement` |

## Dimensionselemente

Jedes Element ist der literale Platzierungswert, der für „Anzeigenstart[&#x200B; gemeldet &#x200B;](/help/implementation/events/ads/ad-start.md).
