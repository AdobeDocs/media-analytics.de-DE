---
title: Ereignisse anhalten
description: Zählt jede einzelne Pause, die während einer Sitzung aufgetreten ist.
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
