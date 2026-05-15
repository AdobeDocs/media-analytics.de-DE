---
title: Inhalt abgeschlossen
description: Zählt Sitzungen, deren Abspielkopf das Ende des Inhalts erreicht hat.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 10%

---


# Inhalt abgeschlossen

Die **Inhalt abgeschlossen** zählt Sitzungen, deren Abspielkopf das Ende des Inhalts erreicht hat. Kombinieren Sie es mit [Inhaltsstarts](content-starts.md) um die Abschlussrate zu berechnen; paaren Sie mit [Medienstarts](media-starts.md) um die End-to-End-Ansichtsrate zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend wird `mediaReporting.sessionDetails.isCompleted = true`, wenn ein [Sitzungs-](/help/implementation/events/session/session-complete.md)&quot; empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet. Eine Sitzung, bei der eine Zeitüberschreitung ohne explizite `sessionComplete` auftritt, wird nicht als Abschluss gezählt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.complete`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.complete` |
