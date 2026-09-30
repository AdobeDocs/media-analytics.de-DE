---
title: Inhaltsstarts
description: Zählt Sitzungen, in denen der Hauptinhalt tatsächlich zu spielen begann.
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
source-wordcount: '148'
ht-degree: 10%
---

# Inhaltsstarts

Die **Inhaltsstartmetrik** zählt Sitzungen, in denen die Wiedergabe des Hauptinhalts tatsächlich begonnen hat. Im Gegensatz [Medienstarts](media-starts.md) werden Sitzungen ausgeschlossen, die während Pre-Roll-Anzeigen, Pufferung oder Stalls endeten. Dies macht ihn zum richtigen Nenner für die Fertigstellungs- und Interaktionsraten.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten [ eines ](/help/implementation/events/playback/play.md)-Ereignisses für den Hauptinhalt. Die Metrik wird bei diesem Wiedergabeereignis ausgelöst, aber beim Schließen-Aufruf gemeldet. Verwenden Sie `(Media starts − Content starts) / Media starts`, um die Abwurfrate vor der Walze zu berechnen.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.play`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.play` |
