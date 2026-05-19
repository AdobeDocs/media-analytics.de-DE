---
title: Besuchszeit für Inhalt
description: Gibt die Gesamtzahl der Sekunden der aktiven Wiedergabe von Hauptinhalten pro Sitzung an.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 6%

---


# Besuchszeit für Inhalt

Die Metrik **Besuchszeit für Inhalt** zeigt die Gesamtsekunden der aktiven Wiedergabe des Hauptinhalts pro Sitzung an, ohne Anzeigen, Pausen, Pufferung und Verzögerungen. Verwenden Sie sie als Interaktionsmetrik für die Anzeige von Inhalten. Informationen zur Besuchszeit einschließlich Anzeigen finden Sie [Besuchszeit für Medien](media-time-spent.md).

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Wanduhrzeit zwischen den Ereignissen, während sich der Player im `play` für den Hauptinhalt befindet. Die Zeit während Anzeigen, Pausen, Pufferereignissen und Anhalten ist ausgeschlossen. Da nur die aktive Wiedergabedauer gezählt wird, kann die Metrik [Inhaltslänge](/help/reporting/dimensions/content-length.md) überschreiten, wenn ein Betrachter ein Segment rückwärts sucht und erneut ansieht. Bei jedem Durchlauf durch ein bestimmtes Segment wird zusätzliche Wiedergabezeit angesammelt. Diese kann anfallen, solange der Benutzer Inhalte in einer Sitzung konsumiert und zurückspult. Die Metrik wird beim Schließen-Aufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und in Sekunden in Daten-Feeds, Data Warehouse und Reporting-APIs angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.timePlayed`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
