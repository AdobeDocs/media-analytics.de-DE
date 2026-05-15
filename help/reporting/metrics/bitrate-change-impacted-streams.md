---
title: Von Bitratenänderung betroffene Streams
description: Zählt Sitzungen, in denen mindestens eine Bitratenänderung aufgetreten ist.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# Von Bitratenänderung betroffene Streams

Die Metrik **Bitratenänderung wirkt sich auf Streams aus** zählt Sitzungen, in denen mindestens eine Bitratenänderung aufgetreten ist. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Bitratenänderungen innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das gesamte Bitratenänderungsvolumen [Bitratenänderungen](/help/reporting/dimensions/bitrate-changes.md).

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true` ersten Mal fest, wenn während [ Sitzung ein ](/help/implementation/events/playback/bitrate-change.md)Bitratenänderungsereignis“ empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateChange`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
