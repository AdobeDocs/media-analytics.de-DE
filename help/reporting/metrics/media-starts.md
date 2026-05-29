---
title: Medienstarts
description: Zählt alle gestarteten Mediensitzungen, einschließlich der Sitzungen, die mit Pre-Roll-Anzeigen oder Pufferung endeten.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 6%

---


# Medienstarts

Die Metrik **Medienstarts** zählt jede Mediensitzung, die begonnen hat. Sie wird inkrementiert, sobald das Backend ein [Sitzungsstart](/help/implementation/events/session/session-start.md)-Ereignis erhält, auch wenn der Viewer während Pre-Roll-Anzeigen, Pufferung oder vor der Wiedergabe von Hauptinhalten ausfällt. Verwenden Sie diese Metrik als umfassendste Top-of-funnel-Metrik für Medienberichte. Kombinieren Sie sie mit [Inhaltsstarts](content-starts.md) um Anzeigen- und Pufferabbrüche zu messen.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn ein [Sitzungsstart](/help/implementation/events/session/session-start.md)-Ereignis empfangen wird. Die gemeldete Metrik ist `1` pro Sitzung. Medienstarts werden beim Start-Aufruf gemeldet, nicht beim Schließen-Aufruf. Es ist die einzige Metrik, die nicht auf den Sitzungsabschluss wartet. Alle anderen Medienmetriken, einschließlich [Inhaltsstarts](/help/reporting/metrics/content-starts.md), [Besuchszeit für Inhalte](/help/reporting/metrics/content-time-spent.md) und [Fortschrittsmarken](/help/reporting/metrics/progress-markers.md) werden beim Schließen-Aufruf gemeldet und sind während der Wiedergabe nicht in Echtzeit verfügbar. [Anzeigenstarts](/help/reporting/metrics/ad-starts.md) ist die eine zusätzliche Metrik, die über das auslösende Ereignis anstatt über den Abschluss gemeldet wird.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.view`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.view` |
