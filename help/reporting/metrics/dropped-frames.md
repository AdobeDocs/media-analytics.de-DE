---
title: Dropped Frames (Metrik)
description: meldet kumulative Dropped Frames für Summen und Durchschnittswerte über Sitzungen hinweg.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Dropped Frames (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Abgelegte Frames**behandelt. Adobe Analytics füllt automatisch eine paarweise [Abgelegte Frames (Dimension](/help/reporting/dimensions/dropped-frames.md) aus derselben `a.media.qoe.droppedFrameCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `mediaReporting.qoeDataDetails.droppedFrames` bereit, das Sie als Dimension oder Metrik verwenden können. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/quality/dropped-frames.md) unter „Abgelegte Frames“*

>[!ENDSHADEBOX]

Die Metrik **Abgelegte Frames** zeigt kumulative abgelegte Frames über Sitzungen hinweg an. Dies ist für Summen, Durchschnittswerte und Perzentil-Rollups geeignet. Verwenden Sie die -Metrik, um das gesamte Ablagevolumen in einem Berichtszeitraum zu berechnen und die Frame-Rendering-Qualität zwischen Inhalten, Netzwerken oder Playern zu vergleichen.

## Berechnung dieser Metrik

Der Player aktualisiert den `droppedFrames` des QoE-Objekts, wenn sich Drops ansammeln. Das Backend meldet den neuesten Wert beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.droppedFrameCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |

Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob Frames überhaupt abgelegt wurden) [von abgelegten Frames betroffene Streams](dropped-frame-impacted-streams.md).
