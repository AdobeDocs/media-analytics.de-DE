---
title: Betroffene Streams angehalten
description: Zählt Sitzungen, in denen der Viewer mindestens einmal pausiert hat.
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
source-wordcount: '152'
ht-degree: 11%
---

# Betroffene Streams angehalten

Die Metrik **Ausgesetzte betroffene Streams** zählt Sitzungen, in denen der Viewer mindestens einmal pausiert hat. Dies ist ein boolescher Wert auf Sitzungsebene. Mehrere Pausen innerhalb derselben Sitzung zählen als ein betroffener Stream. Verwenden Sie diese Option, um den Anteil der Sitzungen zu messen, bei denen eine Pause eintrat. Verwenden Sie für das gesamte Pausenvolumen [Pausenereignisse](pause-events.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn während der Sitzung zum ersten Mal ein [Pause Start](/help/implementation/events/playback/pause-start.md)-Ereignis empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pause`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
