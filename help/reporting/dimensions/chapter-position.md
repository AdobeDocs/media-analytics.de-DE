---
title: Kapitelposition
description: Gibt den Index jedes Kapitels im Inhalt an.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Kapitelposition

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Kapitelposition**&#x200B;behandelt. Siehe [Kapitelposition](/help/implementation/variables/chapters/chapter-position.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Kapitelposition** zeigt den Index jedes Kapitels im Inhalt an.

## So wird diese Dimension ausgefüllt

Die Kapitelposition wird vom Player bei jedem [Kapitelstart](/help/implementation/events/chapters/chapter-start.md) festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.position` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Kapitel](chapter.md). Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.index`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.chapter.position` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.chapter.position` |

## Klassifizierungsansatz

Adobe erstellt die Klassifizierungsstruktur für die Kapitelposition automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Kapitel-ID und ihrer Position. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Namen der Kapitelposition-Klassifizierung. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.position` einer eVar zuordnet. Dieser Ansatz erfasst die Kapitelposition als Wert pro Treffer, ohne dass eine Classification-Wartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen der Kapitelposition und der übergeordneten [Chapter](chapter.md)-Dimension verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Kapitel-ID über Ereignisse hinweg sendet, können unter demselben Kapitel mehrere Positionen angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der ganzzahlige Positionswert, der beim [&#x200B; (Kapitelstart) &#x200B;](/help/implementation/events/chapters/chapter-start.md) wird.
