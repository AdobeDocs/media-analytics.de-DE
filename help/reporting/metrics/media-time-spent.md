---
title: Besuchszeit für Medien
description: Gibt die gesamten Sekunden der aktiven Wiedergabe pro Sitzung an, einschließlich Anzeigen.
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
source-wordcount: '182'
ht-degree: 8%
---

# Besuchszeit für Medien

Die Metrik **Mit Medien verbrachte Zeit** gibt die Gesamtzahl der Sekunden der aktiven Wiedergabe pro Sitzung an, einschließlich Hauptinhalt und Anzeigen, jedoch ohne Pausen, Pufferung und Verzögerungen. Verwende ihn, um die Gesamtzeit zu messen, in der der Betrachter aktiv mit dem Player interagiert hat. Verwenden Sie nur für Hauptinhalte [Besuchszeit für Inhalt](content-time-spent.md).

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Wanduhrzeit zwischen den Ereignissen, während sich der Player im `play` befindet, entweder in Bezug auf Hauptinhalte oder Anzeigen. Die Zeit während der Pausen, Pufferereignisse und Verzögerungen ist ausgeschlossen. Die Metrik wird beim Schließen-Aufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und in Sekunden in Daten-Feeds, Data Warehouse und Reporting-APIs angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.totalTimePlayed`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
