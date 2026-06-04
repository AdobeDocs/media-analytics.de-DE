---
title: Creative-ID
description: Meldet die Kennung der Werbeanzeige.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 3%

---


# Creative-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Creative ID**&#x200B;behandelt. Informationen zum Erfassen dieser Variablen finden [&#128279;](/help/implementation/variables/ads/creative-id.md) unter Creative ID*

>[!ENDSHADEBOX]

Die Dimension **Creative ID** zeigt die ID der Kreativität der Anzeige an. Verwenden Sie die Dimension, um die Interaktion auf alle Anzeigen zu verteilen, die eine kreative Idee gemeinsam haben.

## So wird diese Dimension ausgefüllt

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.creative` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Ad](ad.md) - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.creative` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.ad.creative` |

## Klassifizierungsansatz

Adobe erstellt die Creative ID-Klassifizierungsstruktur automatisch, wenn **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Werbe-ID und ihrer Kreativ-ID. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Creative ID-Klassifizierungsnamen. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.creative` einer eVar zuordnet. Dieser Ansatz erfasst die Kreativ-ID als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen der Kreativ-ID und der übergeordneten [Ad) &#x200B;](ad.md). Wenn Ihre Implementierung inkonsistente Werte für dieselbe Anzeigen-ID über Ereignisse hinweg sendet, können unter derselben Anzeige mehrere kreative IDs angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist eine eindeutige Kreativ-ID. Verwenden Sie eine stabile Kennung pro Kreativ, damit derselbe Kreative in allen Kampagnen auf einen einzelnen Zeileneintrag angewendet wird.
