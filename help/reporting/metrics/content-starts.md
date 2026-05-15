---
title: Inhaltsstarts
description: Zählt Sitzungen, in denen der Hauptinhalt tatsächlich zu spielen begann.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 10%

---


# Inhaltsstarts

Die **Inhaltsstartmetrik** zählt Sitzungen, in denen die Wiedergabe des Hauptinhalts tatsächlich begonnen hat. Im Gegensatz [Medienstarts](media-starts.md) werden Sitzungen ausgeschlossen, die während Pre-Roll-Anzeigen, Pufferung oder Stalls endeten. Dies macht ihn zum richtigen Nenner für die Fertigstellungs- und Interaktionsraten.

## Berechnung dieser Metrik

Das Medien-Backend legt `mediaReporting.sessionDetails.isPlayed = true` ersten Mal ein [Play](/help/implementation/events/playback/play.md)-Ereignis für den Hauptinhalt fest. Die Metrik wird bei diesem Wiedergabeereignis ausgelöst, aber beim Schließen-Aufruf gemeldet. Verwenden Sie `(Media starts − Content starts) / Media starts`, um die Abwurfrate vor der Walze zu berechnen.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.play`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.play` |
