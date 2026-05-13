---
title: Anzeige abgeschlossen
description: Zählt alle Anzeigen, die bis zum Abschluss gespielt wurden.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# Anzeige abgeschlossen

Die Metrik **Anzeige abgeschlossen** zählt jede Anzeige, die bis zum Abschluss gespielt wurde. Kombinieren Sie dies mit [Anzeigenstarts](ad-starts.md) um die Abschlussrate der Anzeige zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.advertisingDetails.isCompleted = true` fest, wenn ein `media.adComplete` empfangen wird. Die Metrik wird beim Aufruf zum Schließen der Anzeige gemeldet. Übersprungene oder abgebrochene Anzeigen werden nicht als Abschlüsse gezählt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.complete`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
