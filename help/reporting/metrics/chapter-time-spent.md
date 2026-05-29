---
title: Besuchszeit für Kapitel
description: Gibt die Gesamtzahl der Sekunden aktiver Wiedergabe pro Kapitel an.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# Besuchszeit für Kapitel

Die Metrik **Besuchszeit für Kapitel** zeigt die gesamten Sekunden der aktiven Wiedergabe pro Kapitel an. Kombinieren Sie sie mit [Kapitellänge](/help/reporting/dimensions/chapter-length.md), um den Anteil jedes verbrauchten Kapitels zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Wanduhrzeit zwischen den Ereignissen, während sich der Player in einem Kapitel im `play` befindet. Die Zeit während der Pausen, Pufferung und des Anhaltens ist ausgeschlossen. Die Metrik wird beim Kapitelabschlussaufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und in Sekunden in Daten-Feeds, Data Warehouse und Reporting-APIs angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.chapter.timePlayed`, wenn [[!UICONTROL Medienkapitel]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
