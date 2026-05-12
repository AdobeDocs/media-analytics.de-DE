---
title: Name des Kapitels
description: Blendet den für Menschen lesbaren Kapiteltitel ein.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# Name des Kapitels

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Kapitelname**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/chapters/chapter-name.md) unter „Kapitelname“*

>[!ENDSHADEBOX]

Die Dimension **Kapitelname** zeigt den für Menschen lesbaren Titel jedes Kapitels an (z. B. `"Pilot Episode - Opening"`).

## So wird diese Dimension ausgefüllt

Der Name des Kapitels wird vom Player bei jedem `media.chapterStart` festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.friendlyName` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Chapter](chapter.md) - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.friendlyName`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.chapter.friendlyName` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |

## Klassifizierungsansatz

Adobe erstellt die Klassifizierungsstruktur für Kapitelnamen automatisch, wenn **[[!UICONTROL Medienkapitel]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Kapitel-ID und ihrem Anzeigenamen. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Klassifizierungsnamen des Kapitels. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapter.friendlyName` einer eVar zuordnet. Dieser Ansatz erfasst den Anzeigenamen als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen dem Kapitelnamen und der übergeordneten Dimension [Chapter](chapter.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Kapitel-ID über Ereignisse hinweg sendet, können mehrere Namen unter demselben Kapitel angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der literale Kapiteltitel, der über `media.chapterStart` berichtet wird.
