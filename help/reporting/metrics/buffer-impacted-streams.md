---
title: Vom Puffer betroffene Streams
description: Zählt Sitzungen, in denen der Player mindestens einmal in einen Pufferstatus übergegangen ist.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 10%

---


# Vom Puffer betroffene Streams

Die Metrik **Vom Puffer betroffene Streams** zählt Sitzungen, in denen der Player mindestens einmal einen Pufferstatus erreicht hat. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Pufferereignisse innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das Gesamtpuffervolumen [Buffer-Ereignisse](buffer-events.md).

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.qoeDataDetails.hasBufferImpactedStreams = true` das erste Mal fest, [ während der Sitzung ein &quot;](/help/implementation/events/playback/buffer-start.md)&quot; empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.buffer`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
