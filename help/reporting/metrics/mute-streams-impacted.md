---
title: Von Stummschaltung betroffene Streams
description: Zählt Sitzungen, in denen der Viewer Audio mindestens einmal stumm geschaltet hat.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---


# Von Stummschaltung betroffene Streams

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Streams, die von der Stummschaltung betroffen sind**behandelt. Unter [Stummschaltung](/help/implementation/variables/player-state/mute.md) erfahren Sie, wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Metrik **Von Stummschaltung betroffene Streams** zählt Sitzungen, bei denen der Viewer Audio mindestens einmal stummgeschaltet hat. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Stummschaltflächen innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für das Gesamtstummschaltungsvolumen [Anzahl Stummschaltungen](mute-count.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten Empfang eines Stummschaltungs-Status-Startereignisses während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.mute.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "mute"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
