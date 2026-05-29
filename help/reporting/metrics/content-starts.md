---
title: Inhaltsstarts
description: Zählt Sitzungen, in denen der Hauptinhalt tatsächlich zu spielen begann.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 10%

---


# Inhaltsstarts

Die **Inhaltsstartmetrik** zählt Sitzungen, in denen die Wiedergabe des Hauptinhalts tatsächlich begonnen hat. Im Gegensatz [Medienstarts](media-starts.md) werden Sitzungen ausgeschlossen, die während Pre-Roll-Anzeigen, Pufferung oder Stalls endeten. Dies macht ihn zum richtigen Nenner für die Fertigstellungs- und Interaktionsraten.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten [ eines ](/help/implementation/events/playback/play.md)-Ereignisses für den Hauptinhalt. Die Metrik wird bei diesem Wiedergabeereignis ausgelöst, aber beim Schließen-Aufruf gemeldet. Verwenden Sie `(Media starts − Content starts) / Media starts`, um die Abwurfrate vor der Walze zu berechnen.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.play`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.play` |
