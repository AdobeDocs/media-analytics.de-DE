---
title: Medienstarts
description: Zählt alle gestarteten Mediensitzungen, einschließlich der Sitzungen, die mit Pre-Roll-Anzeigen oder Pufferung endeten.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# Medienstarts

Die Metrik **Medienstarts** zählt jede Mediensitzung, die begonnen hat. Sie wird inkrementiert, sobald das Backend ein [Sitzungsstart](/help/implementation/events/session/session-start.md)-Ereignis erhält, auch wenn der Viewer während Pre-Roll-Anzeigen, Pufferung oder vor der Wiedergabe von Hauptinhalten ausfällt. Verwenden Sie diese Metrik als umfassendste Top-of-funnel-Metrik für Medienberichte. Kombinieren Sie sie mit [Inhaltsstarts](content-starts.md) um Anzeigen- und Pufferabbrüche zu messen.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.sessionDetails.isViewed = true` fest, wenn ein [Sitzungsstart](/help/implementation/events/session/session-start.md)-Ereignis empfangen wird. Die gemeldete Metrik ist `1` pro Sitzung. Medienstarts werden beim Start-Aufruf gemeldet, nicht beim Schließen-Aufruf. Es ist die einzige Phase-1-Metrik, die nicht auf den Abschluss der Sitzung wartet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.view`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.view` |
