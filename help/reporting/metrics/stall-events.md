---
title: Anhalte-Ereignisse
description: Zählt Standereignisse für Summen und Durchschnittswerte über Sitzungen hinweg.
feature: Metrics
role: User, Admin
source-git-commit: 1278355e0bfc67c635250c426edaf865fb658c37
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 7%

---


# Anhalte-Ereignisse

Die Metrik **Unterbrechungsereignisse** zählt Unterbrechungsereignisse über Sitzungen hinweg und eignet sich für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die -Metrik, um das Gesamtstallvolumen in einem Berichtszeitraum zu berechnen und die Stallstabilität über Inhalte, Netzwerke oder Player hinweg zu vergleichen.

In Customer Journey Analytics können `mediaReporting.qoeDataDetails.stallCount` entweder als Metrik oder als Dimension ohne separate Dimensionskomponente verwendet werden.

## Berechnung dieser Metrik

Das Medien-Backend erhöht die Zählung jedes Mal, wenn für mindestens drei aufeinander folgende Ereignisse keine Abspielkopfbewegung auf dem Hauptinhalt aufgezeichnet wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.qoe.stallCount` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.qoe.stallCount`; siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob es zu einem Verzug gekommen ist) &quot;[&#x200B; betroffene Streams verzögern](stall-impacted-streams.md).
