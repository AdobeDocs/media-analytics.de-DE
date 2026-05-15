---
title: Ereignisse anhalten
description: Zählt jede einzelne Pause, die während einer Sitzung aufgetreten ist.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 12%

---


# Ereignisse anhalten

Die **Pause-Ereignisse**-Metrik zählt jedes einzelne [Pause-Start](/help/implementation/events/playback/pause-start.md)-Ereignis, das während einer Sitzung empfangen wurde, einschließlich mehrerer Pausen innerhalb derselben Sitzung. Kombinieren Sie dies mit [Pausierung insgesamt](total-pause-duration.md), um die durchschnittliche Pausenlänge abzuleiten, und mit [Ausgesetzten betroffenen Streams](paused-impacted-streams.md) um Sitzungen zu zählen, die mindestens einmal pausiert haben.

## Berechnung dieser Metrik

`mediaReporting.sessionDetails.pauseCount` Das Medien-Backend wird bei jedem Start-[-Ereignis ](/help/implementation/events/playback/pause-start.md). Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pauseCount`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
