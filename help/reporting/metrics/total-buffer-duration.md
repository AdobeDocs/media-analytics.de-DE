---
title: Gesamtdauer des Puffers (Metrik)
description: Gibt die kumulierte Pufferzeit für Summen und Durchschnittswerte sitzungsübergreifend an.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Gesamtdauer des Puffers (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Gesamtdauer des Puffers**behandelt. Adobe Analytics füllt automatisch eine paarweise [Gesamtpufferdauer (Dimension)](/help/reporting/dimensions/total-buffer-duration.md) aus derselben `a.media.qoe.bufferTime` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `mediaReporting.qoeDataDetails.bufferTime` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Metrik **Gesamtpufferdauer** zeigt die kumulative Pufferzeit über Sitzungen hinweg an, geeignet für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die Metrik, um die Gesamtzeit zu berechnen, die Kunden in einem Berichtszeitraum auf Puffer verbracht haben.

## Berechnung dieser Metrik

Das Medien-Backend addiert die Dauer jedes Pufferintervalls (von `media.bufferStart` bis zur nächsten Statusänderung). Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bufferTime`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
