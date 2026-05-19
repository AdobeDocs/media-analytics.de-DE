---
title: Gesamtdauer der Verzögerung
description: Berichte über die kumulierte Verweilzeit für Summen und Durchschnittswerte in allen Sitzungen.
feature: Metrics
role: User, Admin
source-git-commit: 1278355e0bfc67c635250c426edaf865fb658c37
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%

---


# Gesamtdauer der Verzögerung

Die Metrik **Gesamtdauer der Verzögerung** zeigt die kumulative Verweilzeit in allen Sitzungen an, geeignet für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die Metrik, um die Gesamtzeit zu berechnen, die Betrachter in einem Berichtszeitraum mit angehaltener Wiedergabe verbracht haben.

In Customer Journey Analytics können `mediaReporting.qoeDataDetails.stallTime` entweder als Metrik oder als Dimension ohne separate Dimensionskomponente verwendet werden.

## Berechnung dieser Metrik

Das Medien-Backend addiert die Dauer jedes Pausenintervalls, das erkannt wird, wenn für mindestens drei aufeinander folgende Ereignisse keine Abspielkopfbewegung auf dem Hauptinhalt aufgezeichnet wird. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.qoe.stallTime` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.qoe.stallTime`; siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
