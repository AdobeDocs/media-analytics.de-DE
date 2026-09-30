---
title: Von Dropped Frames betroffene Streams
description: Zählt Sitzungen, in denen mindestens ein Frame gelöscht wurde.
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
source-wordcount: '135'
ht-degree: 11%
---

# Von Dropped Frames betroffene Streams

Die Metrik **Abgelegter Frame betrifft Streams** zählt Sitzungen, in denen mindestens ein Frame abgelegt wurde. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene. Mehrere Drops innerhalb derselben Sitzung zählen als ein betroffener Stream. Verwenden Sie für das gesamte Ablagevolumen &quot;[&#x200B; Frames](dropped-frames.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn der `droppedFrames` des QoE-Objekts beim Schließen der Sitzung größer als null ist.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.droppedFrames`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
