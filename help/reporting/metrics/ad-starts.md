---
title: Anzeigenstarts
description: Zählt jede Anzeige, die während einer Sitzung zu spielen begann.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---


# Anzeigenstarts

Die Metrik **Anzeigenstart** zählt jede Anzeige, die während einer Sitzung zu spielen begann. Kombinieren Sie dies mit [Anzeige abgeschlossen](ad-completes.md), um die Abschlussrate der Anzeige zu berechnen, und mit [Anzeigenanzahl](/help/reporting/metrics/ad-count.md) für die entsprechende Datenaggregation auf Sitzungsebene.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.advertisingDetails.isStarted = true` fest, wenn ein [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis empfangen wird. Die Metrik wird beim Anzeigenstart-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.view`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
