---
title: Geschätzte Streams
description: Ermittelt die Anzahl der Audio- oder Videostreams pro Sitzung.
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
source-wordcount: '190'
ht-degree: 10%
---

# Geschätzte Streams

Die Metrik **Geschätzte Streams** schätzt die Anzahl der Audio- oder Video-Streams pro Sitzung, wobei alle 30 Minuten der gesamten Wiedergabe ein Stream gezählt wird. Es ist für Content-Syndication-Vereinbarungen gedacht und erreicht Näherungswerte, bei denen jeder 30-minütige Verbrauchsblock als separater „Stream“ zählt.

## Berechnung dieser Metrik

Das Medien-Backend berechnet diese Metrik als `FLOOR(totalTimePlayed / 1800) + 1`, wobei `totalTimePlayed` [Besuchszeit für Medien](media-time-spent.md) in Sekunden ist. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Besuchszeit für Medien | Geschätzte Streams |
| --- | --- |
| 0-29 Min | 1 |
| 30-59 Min | 2 |
| 60-89 Min | 3 |
| 90+ Min | 4+ |

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.estimatedStreams` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.estimatedStreams`; siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
