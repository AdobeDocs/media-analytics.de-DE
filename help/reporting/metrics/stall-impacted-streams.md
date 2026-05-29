---
title: Betroffene Datenströme verzögern
description: Zählt Sitzungen, in denen die Wiedergabe mindestens einmal angehalten wurde.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Betroffene Datenströme verzögern

Die Metrik **Vom Verzug betroffene Streams** zählt Sitzungen, bei denen während der Wiedergabe mindestens ein Verzug aufgetreten ist. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Stände innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das Gesamtvolumen das [Verweilereignisse](stall-events.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn während der Sitzung für mindestens drei aufeinander folgende Ereignisse keine Abspielkopfbewegung auf dem Hauptinhalt aufgezeichnet wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.qoe.stall` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.qoe.stall`; siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
