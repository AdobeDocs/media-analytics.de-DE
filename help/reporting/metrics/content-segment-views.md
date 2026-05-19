---
title: Ansichten des Inhaltssegments
description: Zählt Segmente, in denen die aktive Wiedergabe des Hauptinhalts stattgefunden hat.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 9%

---


# Ansichten des Inhaltssegments

Die Metrik **Inhaltssegmentansichten** zählt fünfminütige Inhaltssegmente, in denen die aktive Wiedergabe von Hauptinhalten stattfand. Die Metrik bestätigt, dass der Viewer Inhalte in diesem Segment abgespielt hat, anstatt sie nur zu laden oder zu puffern. Kombinieren Sie sie mit der Dimension [Inhaltssegment](/help/reporting/dimensions/content-segment.md), um aufzuschlüsseln, welche Teile von Viewern für langfristige Inhalte tatsächlich genutzt werden.

## Berechnung dieser Metrik

Das Medien-Backend setzt diese Markierung für jeden Schließen-Aufruf, der ein Segment abdeckt, in dem mindestens ein [play](/help/implementation/events/playback/play.md)-Ereignis für den Hauptinhalt empfangen wurde. Die Metrik wird beim Schließen-Aufruf gemeldet. Im Pfad der Media Edge-API werden Segmentansichten unter derselben Bedingung ausgelöst, wie Inhalte beginnen. Beide erfordern ein [-](/help/implementation/events/playback/play.md)-Ereignis für Hauptinhalte.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.segmentView`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
