---
title: Gesamtdauer der Verzögerung
description: Berichte über die kumulierte Verweilzeit für Summen und Durchschnittswerte in allen Sitzungen.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%
---

# Gesamtdauer der Verzögerung

Die Metrik **Gesamtdauer der Verzögerung** zeigt die kumulative Verweilzeit in allen Sitzungen an, geeignet für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die Metrik, um die Gesamtzeit zu berechnen, die Betrachter in einem Berichtszeitraum mit angehaltener Wiedergabe verbracht haben.

In Customer Journey Analytics können `xdm.mediaReporting.qoeDataDetails.stallTime` entweder als Metrik oder als Dimension ohne separate Dimensionskomponente verwendet werden.

## Berechnung dieser Metrik

Das Medien-Backend addiert die Dauer jedes Pausenintervalls, das erkannt wird, wenn für mindestens drei aufeinander folgende Ereignisse keine Abspielkopfbewegung auf dem Hauptinhalt aufgezeichnet wird. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.qoe.stallTime` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.qoe.stallTime`; siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
