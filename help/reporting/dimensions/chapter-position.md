---
title: Kapitelposition
description: Gibt den Index jedes Kapitels im Inhalt an.
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
source-wordcount: '368'
ht-degree: 2%
---

# Kapitelposition

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Kapitelposition**behandelt. Siehe [Kapitelposition](/help/implementation/variables/chapters/chapter-position.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Kapitelposition** zeigt den Index jedes Kapitels im Inhalt an.

## So wird diese Dimension ausgefüllt

Die Kapitelposition wird vom Player bei jedem [Kapitelstart](/help/implementation/events/chapters/chapter-start.md) festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.position` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Kapitel](chapter.md). Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.index`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.chapter.position` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.chapter.position` |

## Klassifizierungsansatz

Adobe erstellt die Klassifizierungsstruktur für die Kapitelposition automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[ auszufüllen und zu ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1:1-Beziehung zwischen jeder Kapitel-ID und ihrer Position. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Namen der Kapitelposition-Klassifizierung. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.position` einer eVar zuordnet. Dieser Ansatz erfasst die Kapitelposition als Wert pro Treffer, ohne dass eine Classification-Wartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1:1-Beziehung zwischen der Kapitelposition und der übergeordneten Dimension [Chapter](chapter.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Kapitel-ID über Ereignisse hinweg sendet, können unter demselben Kapitel mehrere Positionen angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der ganzzahlige Positionswert, der beim [ (Kapitelstart) ](/help/implementation/events/chapters/chapter-start.md) wird.
