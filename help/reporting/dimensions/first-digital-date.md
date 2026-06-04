---
title: Erstes digitales Datum
description: Gibt das Datum an, an dem der Inhalt zum ersten Mal auf einer digitalen Plattform angezeigt wurde.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# Erstes digitales Datum

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Berichtsdimension **Erstes digitales Datum**. Siehe [Erstes digitales Datum](/help/implementation/variables/standard-metadata/first-digital-date.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Erstes digitales Datum** zeigt das Datum an, an dem der Inhalt zum ersten Mal auf einer digitalen Plattform erschienen ist. Verwenden Sie ihn zusammen mit [Erstes Sendedatum](first-air-date.md), um den digitalen Veröffentlichungszeitpunkt mit der ursprünglichen Ausstrahlung zu vergleichen.

## So wird diese Dimension ausgefüllt

Das erste digitale Datum wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.digitalDate` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Inhalt (ID)](content.md) - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.digitalDate` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## Klassifizierungsansatz

Adobe erstellt die erste digitale Datumsklassifizierungsstruktur automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Inhalts-ID und dem ersten digitalen Datum. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Namen der ersten digitalen Datumsklassifizierung. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.digitalDate` einer eVar zuordnet. Dieser Ansatz erfasst das erste digitale Datum als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen dem ersten digitalen Datum und der übergeordneten Dimension [Content (ID)](content.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Inhalts-ID über Ereignisse hinweg sendet, können mehrere erste digitale Datumsangaben unter demselben Inhalt angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist die beim Sitzungsbeginn gemeldete Datums-Literalzeichenfolge. Verwenden Sie ein konsistentes Format für alle Implementierungen. Adobe empfiehlt `YYYY-MM-DD`.
