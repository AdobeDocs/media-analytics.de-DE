---
title: Creative-URL
description: Meldet die Asset-URL jeder kreativen Anzeige.
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
source-wordcount: '152'
ht-degree: 10%
---

# Creative-URL

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Berichtsdimension **Creative**&#x200B;URL. Informationen zum Erfassen dieser Variablen finden [&#128279;](/help/implementation/variables/ads/creative-url.md) unter Creative-URL*

>[!ENDSHADEBOX]

Die Dimension **Creative URL** zeigt die Asset-URL jedes Kreativinhalts an. Verwenden Sie die Dimension, wenn die URL selbst für die Analyse von Bedeutung ist (z. B. durch Unterscheidung von CDN-Pfaden oder kreativen Versionen).

## So wird diese Dimension ausgefüllt

Die Creative-URL wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.creativeURL` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.creativeURL` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.ad.creativeURL` |

## Dimensionselemente

Jedes Element ist die literale URL-Zeichenfolge, die beim [Anzeigenstart“ gemeldet &#x200B;](/help/implementation/events/ads/ad-start.md).
