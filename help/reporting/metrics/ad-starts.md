---
title: Anzeigenstarts
description: Zählt jede Anzeige, die während einer Sitzung zu spielen begann.
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
source-wordcount: '126'
ht-degree: 11%
---

# Anzeigenstarts

Die Metrik **Anzeigenstart** zählt jede Anzeige, die während einer Sitzung zu spielen begann. Kombinieren Sie dies mit [Anzeige abgeschlossen](ad-completes.md), um die Abschlussrate der Anzeige zu berechnen, und mit [Anzeigenanzahl](/help/reporting/metrics/ad-count.md) für die entsprechende Datenaggregation auf Sitzungsebene.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn ein [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis empfangen wird. Die Metrik wird beim Anzeigenstart-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.view`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
