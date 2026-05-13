---
title: Gesamte Pausendauer
description: Gibt die kumulierten Sekunden an, die der Betrachter während einer Sitzung pausiert hat.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 8%

---


# Gesamte Pausendauer

Die Metrik **Gesamte Pausendauer** zeigt die kumulativen Sekunden an, die der Viewer während einer Sitzung verbracht hat, um zu pausieren. Die Metrik ist die Summe aller Intervalle zwischen jedem `media.pauseStart` und den nachfolgenden `media.play`. Mehrere Pausen werden hinzugefügt. Kombinieren Sie mit [Pause-](pause-events.md)), um die durchschnittliche Pausenlänge abzuleiten.

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Wanduhrzeit zwischen jedem `media.pauseStart` und dem passenden `media.play`. Die Metrik wird beim Schließen-Aufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und an anderer Stelle in Sekunden angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pauseTime`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
