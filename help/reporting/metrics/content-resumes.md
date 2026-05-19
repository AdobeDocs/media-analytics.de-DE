---
title: Inhaltswiederaufnahmen
description: Zählt Sitzungen, mit denen eine zuvor unterbrochene Wiedergabe fortgesetzt wurde.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 10%

---


# Inhaltswiederaufnahmen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Inhaltswiederaufnahmen**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/content-resumes.md) unter „Inhaltswiederaufnahmen“*

>[!ENDSHADEBOX]

Die Metrik **Inhaltswiederaufnahme** zählt Sitzungen, die eine zuvor unterbrochene Wiedergabe wieder aufgenommen haben. Er wird inkrementiert, wenn der Player eine Sitzung als Wiederaufnahme beim `sessionStart` kennzeichnet (z. B. nach einem Puffer, einer Pause oder einem Anhalten von mehr als 30 Minuten). Trennen Sie damit echte neue Sitzungen von Fortsetzungssitzungen für denselben Viewer und dasselbe Asset.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.sessionDetails.hasResume = true` fest, wenn `mediaCollection.sessionDetails.hasResume` beim Ereignis [Sitzungsstart](/help/implementation/events/session/session-start.md) `true` wird. Der Player muss die Sitzung explizit als Wiederaufnahme kennzeichnen. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.resume`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
