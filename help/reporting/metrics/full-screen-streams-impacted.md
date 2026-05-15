---
title: Vom Vollbildmodus betroffene Streams
description: Zählt Sitzungen, in denen der Viewer mindestens einmal im Vollbildmodus angezeigt wurde.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Vom Vollbildmodus betroffene Streams

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Streams, die vom Vollbildmodus betroffen sind**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/player-state/full-screen.md) im Vollbildmodus*

>[!ENDSHADEBOX]

Die Metrik **Vom Vollbildmodus betroffene Streams** zählt Sitzungen, in denen der Betrachter mindestens einmal in den Vollbildmodus eingetreten ist. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Vollbildeinträge innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für die gesamte Vollbild-Eingabeanzahl [Vollbildanzahl](full-screen-count.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt das `isSet`-Flag in `mediaReporting.states[]`, damit der `fullscreen`-Eintrag `true`, wenn zum ersten Mal ein `media.statesUpdate` mit `fullscreen` in `statesStart` empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.fullscreen.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "fullscreen"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.set` |
