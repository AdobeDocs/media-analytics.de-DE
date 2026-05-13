---
title: Fehlerereignisse
description: Zählt Fehlerereignisse für Summen und Durchschnittswerte über Sitzungen hinweg.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 7%

---


# Fehlerereignisse

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Fehlerereignisse**behandelt. Adobe Analytics füllt automatisch eine gepaarte [Fehlerdimension](/help/reporting/dimensions/errors.md) aus derselben `a.media.qoe.errorCount` Kontextdatenvariablen. Customer Journey Analytics stellt ein einzelnes `mediaReporting.qoeDataDetails.errorCount` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Metrik **Fehlerereignisse** zählt Fehlerereignisse über Sitzungen hinweg und eignet sich für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die Metrik, um das Gesamtfehlervolumen in einem Berichtszeitraum zu berechnen und die Fehlerquoten über Inhalte, Netzwerke oder Player hinweg zu vergleichen.

## Berechnung dieser Metrik

Das Medien-Backend erhöht die Anzahl bei jedem vom Player gemeldeten Fehler. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.errorCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |

Verwenden Sie für das boolesche Reporting auf Sitzungsebene (ob überhaupt ein Fehler aufgetreten ist) [Streams mit Auswirkung auf Fehler](error-impacted-streams.md).
