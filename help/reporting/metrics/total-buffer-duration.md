---
title: Gesamtdauer des Puffers (Metrik)
description: Gibt die kumulierte Pufferzeit für Summen und Durchschnittswerte sitzungsübergreifend an.
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
source-wordcount: '196'
ht-degree: 7%
---

# Gesamtdauer des Puffers (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Gesamtdauer des Puffers**behandelt. Adobe Analytics füllt automatisch eine paarweise [Gesamtpufferdauer (Dimension)](/help/reporting/dimensions/total-buffer-duration.md) aus derselben `a.media.qoe.bufferTime` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.bufferTime` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Metrik **Gesamtpufferdauer** zeigt die kumulative Pufferzeit über Sitzungen hinweg an, geeignet für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die Metrik, um die Gesamtzeit zu berechnen, die Kunden in einem Berichtszeitraum auf Puffer verbracht haben.

## Berechnung dieser Metrik

Das Medien-Backend addiert die Dauer jedes Pufferintervalls (von [Pufferstart](/help/implementation/events/playback/buffer-start.md) bis zur nächsten Statusänderung). Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bufferTime`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |
