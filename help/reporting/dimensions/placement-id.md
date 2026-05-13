---
title: Platzierungs-ID
description: Gibt die Platzierungskennung für jede Anzeige an.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 9%

---


# Platzierungs-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Platzierungs-ID**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/ads/placement-id.md) unter „Platzierungs-ID“*

>[!ENDSHADEBOX]

Die Dimension **Platzierungs-ID** zeigt die Anzeigenplatzierungs-ID an (normalerweise ein Slot oder eine Zone, die in Ihrer Anzeigenserver-Plattform definiert ist). Verwenden Sie die Dimension , um die Interaktion und den Abschluss über Platzierungs-Slots hinweg zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Platzierungs-ID wird vom Player bei jedem `media.adStart` Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.placement` einer eVar zuordnet. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.placement` zugeordnet ist) |

## Dimensionselemente

Jedes Element ist der literale Platzierungswert, der für `media.adStart` gemeldet wird.
