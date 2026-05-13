---
title: Fortschrittsmarken
description: Zählen Sie Sitzungen, deren Abspielkopf jeden von fünf festen Schwellenwerten überschritten hat (10 %, 25 %, 50 %, 75 % und 95 %).
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 7%

---


# Fortschrittsmarken

Die **Fortschrittsmarken** sind fünf separate Metriken, die Sitzungen zählen, deren Abspielkopf jeden von fünf festen Schwellenwerten überschritten hat (10 %, 25 %, 50 %, 75 % und 95 % der Inhaltslänge). Verwenden Sie sie, um Abbrüche über die gesamte Inhaltslaufzeit hinweg zu verfolgen. Kombinieren Sie sie mit [Inhaltsstarts](content-starts.md), um den Anteil der gestarteten Sitzungen zu berechnen, die jeden Milestone erreicht haben.

Jeder Marker wird einmal pro Sitzung ausgelöst und wird beim Seek-Back nicht erneut ausgelöst. Übersprungene Markierungen werden bei der Vorwärtssuche nicht gezählt (z. B. springt ein Betrachter von 5 % auf 60 %, um die Markierungen 10 %, 25 % und 50 % gleichzeitig zu erreichen).

## Wie jeder Marker berechnet wird

Das Medien-Backend wertet den gemeldeten Abspielkopf nach jedem Ereignis gegen `Content length` aus. Wenn der Abspielkopf zum ersten Mal einen Schwellenwert überschreitet, wird der entsprechende `mediaReporting.sessionDetails.hasProgress*` boolesche Wert für den Rest der Sitzung auf `true` gesetzt. Alle fünf Markierungen werden beim Schließen-Aufruf gemeldet.

### 10%-Fortschrittsmarkierung {#progress-10}

Wird ausgelöst, wenn der Abspielkopf zum ersten Mal 10 % der Inhaltslänge erreicht.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.progress10`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |

### 25%-Fortschrittsmarkierung {#progress-25}

Wird ausgelöst, wenn der Abspielkopf zum ersten Mal 25 % der Inhaltslänge erreicht.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.progress25`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |

### 50%-Fortschrittsmarkierung {#progress-50}

Wird ausgelöst, wenn der Abspielkopf zum ersten Mal 50 % der Inhaltslänge erreicht.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.progress50`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |

### 75%-Fortschrittsmarkierung {#progress-75}

Wird ausgelöst, wenn der Abspielkopf zum ersten Mal 75 % der Inhaltslänge erreicht.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.progress75`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |

### 95%-Fortschrittsmarkierung {#progress-95}

Wird ausgelöst, wenn der Abspielkopf zum ersten Mal 95 % der Inhaltslänge erreicht.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.progress95`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |

>[!IMPORTANT]
>
>Fortschrittsmarken erfordern ein Reporting über Abspielköpfe, die ungleich null [Inhaltslänge](/help/reporting/dimensions/content-length.md) sind und präzise sind. Wenn die Inhaltslänge nicht festgelegt, null oder falsch ist, können Markierungen zum falschen Zeitpunkt oder überhaupt nicht ausgelöst werden.
