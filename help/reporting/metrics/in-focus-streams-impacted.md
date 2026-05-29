---
title: Im Fokus befindliche Streams, die von betroffen sind
description: Zählt Sitzungen, in denen der Player mindestens einmal im Fokus war.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---


# Im Fokus befindliche Streams, die von betroffen sind

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Von im Fokus betroffene**&quot; behandelt. Siehe [Im Fokus](/help/implementation/variables/player-state/in-focus.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die **Von im Fokus betroffenen Streams** zählt Sitzungen, in denen der Player mindestens einmal im Fokus war. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Fokusereignisse innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das Gesamtereignisvolumen &quot;[&quot; ](in-focus-count.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten Empfang eines Fokusstatus-Startereignisses während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.infocus.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "inFocus"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.infocus.set` |
