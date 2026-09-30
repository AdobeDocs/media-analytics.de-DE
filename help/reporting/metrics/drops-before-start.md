---
title: Drops vor dem Start
description: Zählt Sitzungen, in denen der Viewer beendet wurde, bevor Hauptinhalte gerendert wurden.
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
source-wordcount: '211'
ht-degree: 7%
---

# Drops vor dem Start

Die **Drops vor Start** zählt Sitzungen, in denen der Viewer beendet wurde, bevor Hauptinhalte gerendert wurden. Die Metrik kennzeichnet einen Abbruch vor dem Abbruch eines Inhalts unabhängig vom Anzeigenverhalten, daher ist sie die beste Messung für den Abbruch eines reinen Vorinhalts. Kombinieren Sie sie mit [Medienstarts](/help/reporting/metrics/media-starts.md) und [Inhaltsstarts](/help/reporting/metrics/content-starts.md) um den Anteil der Sitzungen zu berechnen, die nie einen Inhalts-Frame erzeugt haben.

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag für Sitzungen, die geschlossen werden, ohne jemals ein [-](/help/implementation/events/playback/play.md)-Ereignis im Hauptinhalt zu erzeugen. Die Metrik wird beim Schließen-Aufruf gemeldet. Häufige Szenarien sind: Der Viewer wird während einer Pre-Roll-Anzeige beendet, der Player bleibt in der ersten Pufferphase unbegrenzt stehen oder ein Fehler wird ausgelöst, bevor das erste Ereignis für die Wiedergabe des Hauptinhalts stattfindet. In all diesen Fällen zeichnet die Sitzung einen [Medienstart](/help/reporting/metrics/media-starts.md) auf, jedoch [Inhaltsstart](/help/reporting/metrics/content-starts.md) und keine [Fortschrittsmarken](/help/reporting/metrics/progress-markers.md).

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.dropBeforeStart`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
