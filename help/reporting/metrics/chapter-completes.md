---
title: Kapitel abgeschlossen
description: Zählt alle Kapitel, die bis zum Abschluss gespielt wurden.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# Kapitel abgeschlossen

Die Metrik **Kapitel abgeschlossen** zählt jedes Kapitel, das bis zum Abschluss gespielt wurde. Kombinieren Sie dies mit [Kapitel beginnt](chapter-starts.md), um die Kapitelabschlussrate zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend setzt diese Markierung, wenn ein [chapter complete](/help/implementation/events/chapters/chapter-complete.md)-Ereignis empfangen wird. Die Metrik wird beim Kapitelabschlussaufruf gemeldet. Übersprungene oder abgebrochene Mid-Play-Kapitel zählen nicht als Abschlüsse.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.chapter.complete`, wenn [[!UICONTROL Medienkapitel]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
