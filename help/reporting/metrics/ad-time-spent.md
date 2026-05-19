---
title: Besuchszeit für die Anzeige
description: Gibt die Gesamtzahl der Sekunden der aktiven Anzeigenwiedergabe pro Sitzung an.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.timePlayed`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
