---
title: Inhalt abgeschlossen
description: Zählt Sitzungen, deren Abspielkopf das Ende des Inhalts erreicht hat.
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
source-wordcount: '142'
ht-degree: 10%
---

# Inhalt abgeschlossen

Die **Inhalt abgeschlossen** zählt Sitzungen, deren Abspielkopf das Ende des Inhalts erreicht hat. Kombinieren Sie es mit [Inhaltsstarts](content-starts.md) um die Abschlussrate zu berechnen; paaren Sie mit [Medienstarts](media-starts.md) um die End-to-End-Ansichtsrate zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn ein [Session Complete](/help/implementation/events/session/session-complete.md)-Ereignis empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet. Eine Sitzung, bei der eine Zeitüberschreitung ohne explizite `sessionComplete` auftritt, wird nicht als Abschluss gezählt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.complete`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.complete` |
