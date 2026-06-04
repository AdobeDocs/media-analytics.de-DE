---
title: Dropped Frames (Metrik)
description: meldet kumulative Dropped Frames für Summen und Durchschnittswerte über Sitzungen hinweg.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# Dropped Frames (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Abgelegte Frames**&#x200B;behandelt. Adobe Analytics füllt automatisch eine paarweise [Abgelegte Frames (Dimension](/help/reporting/dimensions/dropped-frames.md) aus derselben `a.media.qoe.droppedFrameCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.droppedFrames` bereit, das Sie als Dimension oder Metrik verwenden können. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/quality/dropped-frames.md) unter „Abgelegte Frames“*

>[!ENDSHADEBOX]

Die Metrik **Abgelegte Frames** zeigt kumulative abgelegte Frames über Sitzungen hinweg an. Dies ist für Summen, Durchschnittswerte und Perzentil-Rollups geeignet. Verwenden Sie die -Metrik, um das gesamte Ablagevolumen in einem Berichtszeitraum zu berechnen und die Frame-Rendering-Qualität zwischen Inhalten, Netzwerken oder Playern zu vergleichen.

## Berechnung dieser Metrik

Der Player aktualisiert den `droppedFrames` des QoE-Objekts, wenn sich Drops ansammeln. Das Backend meldet den neuesten Wert beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.droppedFrameCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob Frames überhaupt abgelegt wurden) [von abgelegten Frames betroffene Streams](dropped-frame-impacted-streams.md).
