---
title: Von verdeckten Untertiteln betroffene Streams
description: Zählt Sitzungen, in denen der Viewer Untertitel mindestens einmal aktiviert hat.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 7%

---


# Von verdeckten Untertiteln betroffene Streams

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Von verdeckten Untertiteln betroffene**) behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/closed-captioning.md) unter „Untertitel“*

>[!ENDSHADEBOX]

Die Metrik **Von Untertiteln betroffene Streams** zählt Sitzungen, in denen der Viewer Untertitel mindestens einmal aktiviert hat. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Untertitel werden in derselben Sitzungsanzahl umgeschaltet wie ein betroffener Stream. Verwenden Sie für das Gesamtvolumen der aktivierten Untertitel [Geschlossene Untertitelanzahl](closed-captioning-count.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt das `isSet`-Flag in `mediaReporting.states[]`, damit der `closedCaptioning`-Eintrag `true`, wenn zum ersten Mal ein `media.statesUpdate` mit `closedCaptioning` in `statesStart` empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.closedcaptioning.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "closedCaptioning"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
