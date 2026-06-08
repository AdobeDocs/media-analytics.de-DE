---
title: Vom Vollbildmodus betroffene Streams
description: Zählt Sitzungen, in denen der Viewer mindestens einmal im Vollbildmodus angezeigt wurde.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Vom Vollbildmodus betroffene Streams

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Streams, die vom Vollbildmodus betroffen sind**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/full-screen.md) im Vollbildmodus*

>[!ENDSHADEBOX]

Die Metrik **Vom Vollbildmodus betroffene Streams** zählt Sitzungen, in denen der Betrachter mindestens einmal in den Vollbildmodus eingetreten ist. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene. Es werden mehrere Vollbildeinträge innerhalb derselben Sitzung gezählt, wie ein betroffener Stream. Verwenden Sie für die gesamte Vollbild-Eingabeanzahl [Vollbildanzahl](full-screen-count.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten Empfang eines Vollbild-Status-Startereignisses während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.fullscreen.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "fullscreen"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.set` |
