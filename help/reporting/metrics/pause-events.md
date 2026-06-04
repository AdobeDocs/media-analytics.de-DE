---
title: Ereignisse anhalten
description: Zählt jede einzelne Pause, die während einer Sitzung aufgetreten ist.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# Ereignisse anhalten

Die **Pause-Ereignisse**-Metrik zählt jedes einzelne [Pause-Start](/help/implementation/events/playback/pause-start.md)-Ereignis, das während einer Sitzung empfangen wurde, einschließlich mehrerer Pausen innerhalb derselben Sitzung. Kombinieren Sie dies mit [Pausierung insgesamt](total-pause-duration.md), um die durchschnittliche Pausenlänge abzuleiten, und mit [Ausgesetzten betroffenen Streams](paused-impacted-streams.md) um Sitzungen zu zählen, die mindestens einmal pausiert haben.

## Berechnung dieser Metrik

Das Medien-Backend erhöht diese Anzahl bei jedem [-Start-](/help/implementation/events/playback/pause-start.md). Eine einzelne kontinuierliche Pause generiert unabhängig von ihrer Dauer ein Inkrement. Heartbeat [pings](/help/implementation/events/playback/ping.md) gesendet, während der Player angehalten bleibt, gehören alle zur selben Pausenzeit und erhöhen die Anzahl nicht erneut. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pauseCount`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
