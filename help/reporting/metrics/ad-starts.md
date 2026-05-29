---
title: Anzeigenstarts
description: Zählt jede Anzeige, die während einer Sitzung zu spielen begann.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 11%

---


# Anzeigenstarts

Die Metrik **Anzeigenstart** zählt jede Anzeige, die während einer Sitzung zu spielen begann. Kombinieren Sie dies mit [Anzeige abgeschlossen](ad-completes.md), um die Abschlussrate der Anzeige zu berechnen, und mit [Anzeigenanzahl](/help/reporting/metrics/ad-count.md) für die entsprechende Datenaggregation auf Sitzungsebene.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn ein [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis empfangen wird. Die Metrik wird beim Anzeigenstart-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.view`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
