---
title: Von Bitratenänderung betroffene Streams
description: Zählt Sitzungen, in denen mindestens eine Bitratenänderung aufgetreten ist.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 10%

---


# Von Bitratenänderung betroffene Streams

Die Metrik **Bitratenänderung wirkt sich auf Streams aus** zählt Sitzungen, in denen mindestens eine Bitratenänderung aufgetreten ist. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Bitratenänderungen innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das gesamte Bitratenänderungsvolumen [Bitratenänderungen](/help/reporting/dimensions/bitrate-changes.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn während der Sitzung zum ersten [&#x200B; eine &#x200B;](/help/implementation/events/playback/bitrate-change.md) (Bitratenänderung) empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateChange`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
