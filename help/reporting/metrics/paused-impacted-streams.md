---
title: Betroffene Streams angehalten
description: Zählt Sitzungen, in denen der Viewer mindestens einmal pausiert hat.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 11%

---


# Betroffene Streams angehalten

Die Metrik **Ausgesetzte betroffene Streams** zählt Sitzungen, in denen der Viewer mindestens einmal pausiert hat. Dies ist ein boolescher Wert auf Sitzungsebene. Mehrere Pausen innerhalb derselben Sitzung zählen als ein betroffener Stream. Verwenden Sie diese Option, um den Anteil der Sitzungen zu messen, bei denen eine Pause eintrat. Verwenden Sie für das gesamte Pausenvolumen [Pausenereignisse](pause-events.md).

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.sessionDetails.hasPauseImpactedStreams = true` das erste Mal fest[&#x200B; dass während der Sitzung ein &#x200B;](/help/implementation/events/playback/pause-start.md)-Ereignis empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pause`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
