---
title: Gesamte Pausendauer
description: Gibt die kumulierten Sekunden an, die der Betrachter während einer Sitzung pausiert hat.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---


# Gesamte Pausendauer

Die Metrik **Gesamte Pausendauer** zeigt die kumulativen Sekunden an, die der Viewer während einer Sitzung verbracht hat, um zu pausieren. Die Metrik ist die Summe aller Intervalle zwischen jedem [-Start](/help/implementation/events/playback/pause-start.md)-Ereignis und dem nachfolgenden [-](/help/implementation/events/playback/play.md)-Ereignis. Mehrere Pausen werden hinzugefügt. Kombinieren Sie mit [Pause-](pause-events.md)), um die durchschnittliche Pausenlänge abzuleiten.

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Wanduhrzeit zwischen jedem [Pause-Start](/help/implementation/events/playback/pause-start.md)-Ereignis und dem passenden [Play](/help/implementation/events/playback/play.md)-Ereignis. Die Metrik wird beim Schließen-Aufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und an anderer Stelle in Sekunden angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pauseTime`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
