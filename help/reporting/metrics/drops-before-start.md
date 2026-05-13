---
title: Drops vor dem Start
description: Zählt Sitzungen, in denen der Viewer beendet wurde, bevor Hauptinhalte gerendert wurden.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 8%

---


# Drops vor dem Start

Die **Drops vor Start** zählt Sitzungen, in denen der Viewer beendet wurde, bevor Hauptinhalte gerendert wurden. Die Metrik kennzeichnet einen Abbruch vor dem Abbruch eines Inhalts unabhängig vom Anzeigenverhalten, daher ist sie die beste Messung für den Abbruch eines reinen Vorinhalts. Kombinieren Sie sie mit [Medienstarts](/help/reporting/metrics/media-starts.md) und [Inhaltsstarts](/help/reporting/metrics/content-starts.md) um den Anteil der Sitzungen zu berechnen, die nie einen Inhalts-Frame erzeugt haben.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.qoeDataDetails.isDroppedBeforeStart = true` für Sitzungen fest, die geschlossen werden, ohne dass jemals ein `media.play`-Ereignis zum Hauptinhalt erzeugt wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.dropBeforeStart`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
