---
title: Site-ID
description: Gibt für jede Anzeige die Kennung der Anzeigenseite aus.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 9%

---


# Site-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Site-ID**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/site-id.md) unter „Site-ID“*

>[!ENDSHADEBOX]

Die Dimension **Site-ID** zeigt die ID der Anzeigenwebsite an (normalerweise eine ID aus Ihrer Anzeigenserverplattform). Verwenden Sie die Dimension, um die Interaktion nach Anzeigenplatzierungs-Site aufzuheben.

## So wird diese Dimension ausgefüllt

Die Site-ID wird vom Player bei jedem `media.adStart` Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.site` einer eVar zuordnet. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.site` zugeordnet ist) |

## Dimensionselemente

Jedes Element ist der literale Site-ID-Wert, der für `media.adStart` gemeldet wird.
