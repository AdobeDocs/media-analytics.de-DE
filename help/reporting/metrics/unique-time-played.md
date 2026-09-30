---
title: Eindeutige Wiedergabedauer
description: Gibt die Sekunden bestimmter Inhalte an, die während einer Sitzung angesehen wurden, wobei Suchwiederholungen dedupliziert werden.
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
source-wordcount: '180'
ht-degree: 8%
---

# Eindeutige Wiedergabedauer

Die Metrik **Eindeutige Wiedergabedauer** gibt die Sekunden eindeutiger Inhalte an, die während einer Sitzung angezeigt wurden, wobei Segmente dedupliziert werden, die über das Seek-back wiedergegeben wurden. Im Vergleich zu [Besuchszeit für Inhalte](content-time-spent.md) ist die Wiedergabedauer für Unique Time niedriger, wenn ein Betrachter einen Teil desselben Inhalts innerhalb derselben Sitzung erneut ansieht.

## Berechnung dieser Metrik

Das Medien-Backend verfolgt, welche Abspielkopfintervalle während der Sitzung angesehen wurden, und fasst ihre Vereinigung zusammen. Wenn Sie dasselbe 5-Sekunden-Segment zweimal wiedergeben, zählt dies immer noch als fünf Sekunden. Die Metrik wird beim Schließen-Aufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und in Sekunden in Daten-Feeds, Data Warehouse und Reporting-APIs angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.uniqueTimePlayed`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
