---
title: Anzeigenstarts
description: Zählt jede Anzeige, die während einer Sitzung zu spielen begann.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---


# Anzeigenstarts

Die Metrik **Anzeigenstart** zählt jede Anzeige, die während einer Sitzung zu spielen begann. Kombinieren Sie dies mit [Anzeige abgeschlossen](ad-completes.md), um die Abschlussrate der Anzeige zu berechnen, und mit [Anzeigenanzahl](/help/reporting/metrics/ad-count.md) für die entsprechende Datenaggregation auf Sitzungsebene.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.advertisingDetails.isStarted = true` fest, wenn ein `media.adStart` empfangen wird. Die Metrik wird beim Anzeigenstart-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.view`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
