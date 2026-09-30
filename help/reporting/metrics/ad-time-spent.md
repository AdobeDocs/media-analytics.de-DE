---
title: Besuchszeit für die Anzeige
description: Gibt die Gesamtzahl der Sekunden der aktiven Anzeigenwiedergabe pro Sitzung an.
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
source-wordcount: '174'
ht-degree: 8%
---

# Besuchszeit für die Anzeige

Die Metrik **Besuchszeit für Anzeigen** gibt die Gesamtzahl der Sekunden der aktiven Anzeigenwiedergabe pro Sitzung an, ohne Pausen, Pufferung und Verzögerungen. Kombinieren Sie sie mit [Besuchszeit für Inhalte](/help/reporting/metrics/content-time-spent.md), um die Anzeigenlast mit der Interaktion mit Inhalten zu vergleichen.

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Wanduhrzeit zwischen den Ereignissen, während sich der Player im `play` einer Anzeige befindet. Die Zeit während Pausen, Pufferung und Suchen wird ausgeschlossen, entsprechend der Berechnung [Besuchszeit für Inhalt](/help/reporting/metrics/content-time-spent.md) für den Hauptinhalt. Die Metrik wird beim Aufruf zum Schließen der Anzeige gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und in Sekunden in Daten-Feeds, Data Warehouse und Reporting-APIs angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.timePlayed`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
