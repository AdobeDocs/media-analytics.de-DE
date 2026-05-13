---
title: Kapitel abgeschlossen
description: Zählt alle Kapitel, die bis zum Abschluss gespielt wurden.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# Kapitel abgeschlossen

Die Metrik **Kapitel abgeschlossen** zählt jedes Kapitel, das bis zum Abschluss gespielt wurde. Kombinieren Sie dies mit [Kapitel beginnt](chapter-starts.md), um die Kapitelabschlussrate zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.chapterDetails.isCompleted = true` fest, wenn ein `media.chapterComplete` empfangen wird. Die Metrik wird beim Kapitelabschlussaufruf gemeldet. Übersprungene oder abgebrochene Mid-Play-Kapitel zählen nicht als Abschlüsse.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.chapter.complete`, wenn [[!UICONTROL Medienkapitel]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
