---
title: Betroffene Datenströme verzögern
description: Zählt Sitzungen, in denen die Wiedergabe mindestens einmal angehalten wurde.
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
source-wordcount: '178'
ht-degree: 8%
---

# Betroffene Datenströme verzögern

Die Metrik **Vom Verzug betroffene Streams** zählt Sitzungen, bei denen während der Wiedergabe mindestens ein Verzug aufgetreten ist. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene. Mehrere Stände innerhalb derselben Sitzung zählen als ein betroffener Stream. Verwenden Sie für das Gesamtvolumen das [Verweilereignisse](stall-events.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn während der Sitzung für mindestens drei aufeinander folgende Ereignisse keine Abspielkopfbewegung auf dem Hauptinhalt aufgezeichnet wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.qoe.stall` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.qoe.stall`; siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
