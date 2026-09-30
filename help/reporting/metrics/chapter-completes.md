---
title: Kapitel abgeschlossen
description: Zählt alle Kapitel, die bis zum Abschluss gespielt wurden.
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
source-wordcount: '123'
ht-degree: 12%
---

# Kapitel abgeschlossen

Die Metrik **Kapitel abgeschlossen** zählt jedes Kapitel, das bis zum Abschluss gespielt wurde. Kombinieren Sie dies mit [Kapitel beginnt](chapter-starts.md), um die Kapitelabschlussrate zu berechnen.

## Berechnung dieser Metrik

Das Medien-Backend setzt diese Markierung, wenn ein [chapter complete](/help/implementation/events/chapters/chapter-complete.md)-Ereignis empfangen wird. Die Metrik wird beim Kapitelabschlussaufruf gemeldet. Übersprungene oder abgebrochene Mid-Play-Kapitel zählen nicht als Abschlüsse.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.chapter.complete`, wenn [[!UICONTROL Medienkapitel]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
