---
title: Geschätzte Streams
description: Ermittelt die Anzahl der Audio- oder Videostreams pro Sitzung.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 10%

---


# Geschätzte Streams

Die Metrik **Geschätzte Streams** schätzt die Anzahl der Audio- oder Video-Streams pro Sitzung, wobei alle 30 Minuten der gesamten Wiedergabe ein Stream gezählt wird. Es ist für Content-Syndication-Vereinbarungen gedacht und erreicht Näherungswerte, bei denen jeder 30-minütige Verbrauchsblock als separater „Stream“ zählt.

## Berechnung dieser Metrik

Das Medien-Backend berechnet `mediaReporting.sessionDetails.estimatedStreams = FLOOR(totalTimePlayed / 1800) + 1`, wobei `totalTimePlayed` [Besuchszeit für Medien](media-time-spent.md) in Sekunden ist. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Besuchszeit für Medien | Geschätzte Streams |
| --- | --- |
| 0-29 Min | 1 |
| 30-59 Min | 2 |
| 60-89 Min | 3 |
| 90+ Min | 4+ |

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.estimatedStreams` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.estimatedStreams`; siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
