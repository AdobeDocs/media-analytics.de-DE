---
title: Versatz des Kapitels
description: Gibt den Versatz der einzelnen Kapitel im Inhalt an.
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
source-wordcount: '376'
ht-degree: 2%
---

# Versatz des Kapitels

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Kapitelversatz**&#x200B;behandelt. Siehe [Kapitelversatz](/help/implementation/variables/chapters/chapter-offset.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Kapitelversatz** zeigt den Versatz jedes Kapitels innerhalb des Inhalts in Sekunden ab Beginn an.

## So wird diese Dimension ausgefüllt

Der Kapitelversatz wird vom Player bei jedem [Kapitelstart](/help/implementation/events/chapters/chapter-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.offset` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Kapitel](chapter.md). Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.chapter.offset` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.chapter.offset` |

## Klassifizierungsansatz

Adobe erstellt die Klassifizierungsstruktur für den Kapitelversatz automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1:1-Beziehung zwischen jeder Kapitel-ID und ihrem Offset. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Klassifizierungsnamen für den Kapitelversatz. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.offset` einer eVar zuordnet. Dieser Ansatz erfasst den Kapitelversatz als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1:1-Beziehung zwischen dem Kapitelversatz und der übergeordneten Dimension [Kapitel](chapter.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Kapitel-ID über Ereignisse hinweg sendet, können unter demselben Kapitel mehrere Versätze angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der ganzzahlige Versatzwert in Sekunden, der beim [Kapitelstart“ &#x200B;](/help/implementation/events/chapters/chapter-start.md) wird.
