---
title: Kapitellänge
description: Gibt die Dauer jedes Kapitels an.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# Kapitellänge

>[!BEGINSHADEBOX]

*Diese Seite deckt die Berichtsdimension **Kapitellänge**&#x200B;ab. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/chapters/chapter-length.md) unter „Kapitellänge“*

>[!ENDSHADEBOX]

Die Dimension **Kapitellänge** zeigt die Dauer jedes Kapitels in Sekunden an.

## So wird diese Dimension ausgefüllt

Die Kapitellänge wird vom Player bei jedem [Kapitelstart](/help/implementation/events/chapters/chapter-start.md) festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.length` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Chapter](chapter.md) - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.chapter.length` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.chapter.length` |

## Klassifizierungsansatz

Adobe erstellt die Klassifizierungsstruktur für die Kapitellänge automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Kapitel-ID und ihrer Länge. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Classification-Namen der Kapitellänge. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.length` einer eVar zuordnet. Dieser Ansatz erfasst die Kapitellänge als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen der Kapitellänge und der übergeordneten [Chapter](chapter.md)-Dimension verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Kapitel-ID über Ereignisse hinweg sendet, können unter demselben Kapitel mehrere Längen angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der ganzzahlige Längenwert in Sekunden, der beim [&#x200B; (Kapitelstart) &#x200B;](/help/implementation/events/chapters/chapter-start.md) wird.
