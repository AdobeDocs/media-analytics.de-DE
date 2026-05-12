---
title: Pod-Position
description: Meldet den Versatz jeder Anzeigenunterbrechung im Inhalt.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---


# Pod-Position

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Pod-Position**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden Sie &#x200B;](/help/implementation/variables/ads/ad-break-start-time.md) „Startzeit der Werbeunterbrechung“*

>[!ENDSHADEBOX]

Die Dimension **Pod-Position** zeigt den Versatz jeder Werbeunterbrechung innerhalb des Inhalts in Sekunden an. Ein Pre-Roll hat Position `0`; Mid-Rolls haben Positionen, die ihrer Abspielkopf-Startzeit entsprechen.

## So wird diese Dimension ausgefüllt

Die Pod-Position wird anhand des Werts [Startzeit der Werbeunterbrechung](/help/implementation/variables/ads/ad-break-start-time.md) festgelegt, den der Player für `media.adBreakStart` festlegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.podSecond` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Ad Pod](ad-pod.md) - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.ad.podSecond` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |

## Klassifizierungsansatz

Adobe erstellt die Pod-Positionsklassifizierungsstruktur automatisch, wenn **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Anzeigen-Pod-ID und ihrer Position. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Pod-Positionsklassifizierungsnamen. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.ad.podSecond` einer eVar zuordnet. Dieser Ansatz erfasst die Pod-Position als Wert pro Treffer, ohne dass eine Classification-Wartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen der Pod-Position und der übergeordneten Dimension [Ad Pod](ad-pod.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Pod-ID über Ereignisse hinweg sendet, können mehrere Positionen unter demselben Anzeigen-Pod angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der ganzzahlige Offset-Wert (in Sekunden), der für `media.adBreakStart` gemeldet wird.
