---
title: Kapitelstarts
description: Zählt jedes Kapitel, das während einer Sitzung zu spielen begann.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---


# Kapitelstarts

Die Metrik **Kapitel beginnt** zählt jedes Kapitel, das während einer Sitzung zu spielen begann. Kombinieren Sie dies mit [Kapitel abgeschlossen](chapter-completes.md), um die Kapitelabschlussrate zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend setzt diese Markierung, wenn ein [Kapitelstart](/help/implementation/events/chapters/chapter-start.md)-Ereignis empfangen wird. Die Metrik wird beim Kapitelabschlussaufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.chapter.view`, wenn [[!UICONTROL Medienkapitel]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
