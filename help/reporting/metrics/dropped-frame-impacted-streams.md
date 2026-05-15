---
title: Von Dropped Frames betroffene Streams
description: Zählt Sitzungen, in denen mindestens ein Frame gelöscht wurde.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 11%

---


# Von Dropped Frames betroffene Streams

Die Metrik **Abgelegter Frame betrifft Streams** zählt Sitzungen, in denen mindestens ein Frame abgelegt wurde. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Drops innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das gesamte Ablagevolumen &quot;[&#x200B; Frames](dropped-frames.md).

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams = true` fest, wenn der `droppedFrames` des QoE-Objekts beim Schließen der Sitzung größer als null ist.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.droppedFrames`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
