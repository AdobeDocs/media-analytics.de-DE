---
title: Eindeutige Wiedergabedauer
description: Gibt die Sekunden bestimmter Inhalte an, die während einer Sitzung angesehen wurden, wobei Suchwiederholungen dedupliziert werden.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# Eindeutige Wiedergabedauer

Die Metrik **Eindeutige Wiedergabedauer** gibt die Sekunden eindeutiger Inhalte an, die während einer Sitzung angezeigt wurden, wobei Segmente dedupliziert werden, die über das Seek-back wiedergegeben wurden. Im Vergleich zu [Besuchszeit für Inhalte](content-time-spent.md) ist die Wiedergabedauer für Unique Time niedriger, wenn ein Betrachter einen Teil desselben Inhalts innerhalb derselben Sitzung erneut ansieht.

## Berechnung dieser Metrik

Das Medien-Backend verfolgt, welche Abspielkopfintervalle während der Sitzung angesehen wurden, und fasst ihre Vereinigung zusammen. Wenn Sie dasselbe 5-Sekunden-Segment zweimal wiedergeben, zählt dies immer noch als fünf Sekunden. Die Metrik wird beim Schließen-Aufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und in Sekunden in Daten-Feeds, Data Warehouse und Reporting-APIs angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.uniqueTimePlayed`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
