---
title: Creative-URL
description: Meldet die Asset-URL jeder kreativen Anzeige.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 10%

---


# Creative-URL

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Berichtsdimension **Creative**URL. Informationen zum Erfassen dieser Variablen finden ](/help/implementation/variables/ads/creative-url.md) unter [Creative-URL*

>[!ENDSHADEBOX]

Die Dimension **Creative URL** zeigt die Asset-URL jedes Kreativinhalts an. Verwenden Sie die Dimension, wenn die URL selbst für die Analyse von Bedeutung ist (z. B. durch Unterscheidung von CDN-Pfaden oder kreativen Versionen).

## So wird diese Dimension ausgefüllt

Die Creative-URL wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.creativeURL` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.creativeURL` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.ad.creativeURL` |

## Dimensionselemente

Jedes Element ist die literale URL-Zeichenfolge, die beim [Anzeigenstart“ gemeldet ](/help/implementation/events/ads/ad-start.md).
