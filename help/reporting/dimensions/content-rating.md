---
title: Bewertung des Inhalts
description: Gibt die Zielgruppenbewertung an, wie in den TV Parental Guidelines oder einem regionalen Bewertungssystem definiert.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---


# Bewertung des Inhalts

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Inhaltsbewertung**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/content-rating.md) unter „Inhaltsbewertung“*

>[!ENDSHADEBOX]

Die Dimension **Inhaltsbewertung** gibt die Zielgruppenbewertung für jede Sitzung an. Verwenden Sie diese Option, um die Interaktion und Anzeigenlast über verschiedene Bewertungsebenen hinweg zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Inhaltsbewertung wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.rating` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Inhalt (ID](content.md) . Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.rating` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.rating` |

## Klassifizierungsansatz

Adobe erstellt die Klassifizierungsstruktur für Inhaltsbewertungen automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[ auszufüllen und zu ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1:1-Beziehung zwischen jeder Inhalts-ID und ihrer Bewertung. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Namen der Klassifizierung für die Inhaltsbewertung. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.rating` einer eVar zuordnet. Dieser Ansatz erfasst die Inhaltsbewertung als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass die garantierte 1::1-Beziehung zwischen der Inhaltsbewertung und der übergeordneten Dimension [Inhalt (ID)](content.md) verloren geht. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Inhalts-ID über Ereignisse hinweg sendet, können unter demselben Inhalt mehrere Bewertungen angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der bei Sitzungsbeginn gemeldete literale Bewertungswert (z. B. `"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`). Halten Sie sich an einen festen Satz von Werten pro Bewertungssystem, um die Fragmentierung von Zeilenelementen zu vermeiden.
