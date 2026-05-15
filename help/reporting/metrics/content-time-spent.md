---
title: Besuchszeit für Inhalt
description: Gibt die Gesamtzahl der Sekunden der aktiven Wiedergabe von Hauptinhalten pro Sitzung an.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 8%

---


# Besuchszeit für Inhalt

Die Metrik **Besuchszeit für Inhalt** zeigt die Gesamtsekunden der aktiven Wiedergabe des Hauptinhalts pro Sitzung an, ohne Anzeigen, Pausen, Pufferung und Verzögerungen. Verwenden Sie sie als Interaktionsmetrik für die Anzeige von Inhalten. Informationen zur Besuchszeit einschließlich Anzeigen finden Sie [Besuchszeit für Medien](media-time-spent.md).

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Wanduhrzeit zwischen den Ereignissen, während sich der Player im `play` für den Hauptinhalt befindet. Die Zeit während Anzeigen, Pausen, Pufferereignissen und Anhalten ist ausgeschlossen. Die Metrik wird beim Schließen-Aufruf gemeldet. Der Wert wird in Analysis Workspace als `HH:MM:SS` und in Sekunden in Daten-Feeds, Data Warehouse und Reporting-APIs angezeigt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.timePlayed`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
