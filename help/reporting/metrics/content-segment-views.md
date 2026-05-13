---
title: Ansichten des Inhaltssegments
description: Zählt Segmente, in denen die aktive Wiedergabe des Hauptinhalts stattgefunden hat.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 7%

---


# Ansichten des Inhaltssegments

Die Metrik **Inhaltssegmentansichten** zählt fünfminütige Inhaltssegmente, in denen die aktive Wiedergabe von Hauptinhalten stattfand. Die Metrik bestätigt, dass der Viewer Inhalte in diesem Segment abgespielt hat, anstatt sie nur zu laden oder zu puffern. Kombinieren Sie sie mit der Dimension [Inhaltssegment](/help/reporting/dimensions/content-segment.md), um aufzuschlüsseln, welche Teile von Viewern für langfristige Inhalte tatsächlich genutzt werden.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.sessionDetails.hasSegmentView = true` für jeden Close-Aufruf fest, der ein Segment abdeckt, in dem mindestens ein `media.play` für den Hauptinhalt empfangen wurde. Die Metrik wird beim Schließen-Aufruf gemeldet. Im Pfad der Media Edge-API werden Segmentansichten unter derselben Bedingung ausgelöst, wie Inhalte beginnen. Beide erfordern eine `media.play` auf Hauptinhalte.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.segmentView`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
