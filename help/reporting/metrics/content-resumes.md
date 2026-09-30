---
title: Inhaltswiederaufnahmen
description: Zählt Sitzungen, mit denen eine zuvor unterbrochene Wiedergabe fortgesetzt wurde.
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
source-wordcount: '171'
ht-degree: 9%
---

# Inhaltswiederaufnahmen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Inhaltswiederaufnahmen**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/core/content-resumes.md) unter „Inhaltswiederaufnahmen“*

>[!ENDSHADEBOX]

Die Metrik **Inhaltswiederaufnahme** zählt Sitzungen, die eine zuvor unterbrochene Wiedergabe wieder aufgenommen haben. Er wird inkrementiert, wenn der Player eine Sitzung als Wiederaufnahme beim `sessionStart` kennzeichnet (z. B. nach einem Puffer, einer Pause oder einem Anhalten von mehr als 30 Minuten). Trennen Sie damit echte neue Sitzungen von Fortsetzungssitzungen für denselben Viewer und dasselbe Asset.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag, wenn `xdm.mediaCollection.sessionDetails.hasResume` beim [Sitzungsstart](/help/implementation/events/session/session-start.md)-Ereignis `true` wird. Der Player muss die Sitzung explizit als Wiederaufnahme kennzeichnen. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.resume`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | nicht angegeben |
