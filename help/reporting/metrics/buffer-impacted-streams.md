---
title: Vom Puffer betroffene Streams
description: Zählt Sitzungen, in denen der Player mindestens einmal in einen Pufferstatus übergegangen ist.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

---


# Vom Puffer betroffene Streams

Die Metrik **Vom Puffer betroffene Streams** zählt Sitzungen, in denen der Player mindestens einmal einen Pufferstatus erreicht hat. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene. Es werden mehrere Pufferereignisse innerhalb derselben Sitzung gezählt, wie ein betroffener Stream. Verwenden Sie für das Gesamtpuffervolumen [Buffer-Ereignisse](buffer-events.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten [&#x200B; eines &#x200B;](/help/implementation/events/playback/buffer-start.md)-Ereignisses während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.buffer`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
