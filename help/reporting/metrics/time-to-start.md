---
title: Zeit bis zum Start (Metrik)
description: Gibt die Startzeit für Summen und Durchschnittswerte sitzungsübergreifend an.
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
source-wordcount: '202'
ht-degree: 7%
---

# Zeit bis zum Start (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Zeit bis zum Start**&#x200B;behandelt. Adobe Analytics füllt automatisch eine paarweise [Time to Start (Dimension](/help/reporting/dimensions/time-to-start.md) aus derselben `a.media.qoe.timeToStart` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.timeToStart` bereit, das Sie als Dimension oder Metrik verwenden können. Informationen [&#x200B; Erfassen dieser Variablen finden Sie &#x200B;](/help/implementation/variables/quality/time-to-start.md) „Zeit bis zum Start“*

>[!ENDSHADEBOX]

Die **Time to Start**-Metrik meldet die Startzeit sitzungsübergreifend und eignet sich für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die -Metrik, um die durchschnittliche Startzeit für einen Berichtszeitraum zu berechnen und die Startleistung in allen Inhalten, Netzwerken oder Playern zu vergleichen. Adobe speichert den Wert in Sekunden und konvertiert bei der Aufnahme die Millisekunden, die der Player meldet.

## Berechnung dieser Metrik

Der Player legt `timeToStart` auf das QoE-Objekt fest, bevor der Sitzungsstart ausgelöst wird. Das Backend meldet den Wert beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.timeToStart`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
