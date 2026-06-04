---
title: Von Fehlern betroffene Streams
description: Zählt Sitzungen, in denen mindestens ein Fehler aufgetreten ist.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# Von Fehlern betroffene Streams

Die Metrik **Vom Fehler betroffene Streams** zählt Sitzungen, in denen mindestens ein Fehler aufgetreten ist (`trackError` wurde aufgerufen oder ein [Fehler](/help/implementation/events/error.md)-Ereignis ausgelöst). Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Fehler innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das gesamte Fehlervolumen [Fehler](/help/reporting/dimensions/errors.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten [&#x200B; (Fehler](/help/implementation/events/error.md)-Ereignis während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.error`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
