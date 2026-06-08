---
title: Von verdeckten Untertiteln betroffene Streams
description: Zählt Sitzungen, in denen der Viewer Untertitel mindestens einmal aktiviert hat.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# Von verdeckten Untertiteln betroffene Streams

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Von verdeckten Untertiteln betroffene**) behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/closed-captioning.md) unter „Untertitel“*

>[!ENDSHADEBOX]

Die Metrik **Von Untertiteln betroffene Streams** zählt Sitzungen, in denen der Viewer Untertitel mindestens einmal aktiviert hat. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene. Bei der Anzahl mehrerer Untertitel wird dieselbe Sitzung umgeschaltet wie bei einem betroffenen Stream. Verwenden Sie für das Gesamtvolumen der aktivierten Untertitel [Geschlossene Untertitelanzahl](closed-captioning-count.md).

## Berechnung dieser Metrik

Das Medien-Backend legt dieses Flag fest, wenn während der Sitzung zum ersten Mal ein Ereignis zum Aktivieren des Untertitelstatus empfangen wird. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.closedcaptioning.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "closedCaptioning"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.set` |
