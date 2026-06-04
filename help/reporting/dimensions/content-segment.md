---
title: Inhaltssegment
description: Gibt den während einer Sitzung angezeigten Abspielkopfbereich in Minuten an.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# Inhaltssegment

Die Dimension **Inhaltssegment** zeigt den während einer Sitzung angezeigten Abspielkopfbereich in Minuten an (z. B. `[0-5]` für die Minuten 0 bis 5). Das Backend berechnet das Segment aus den minimalen und maximalen Abspielkopfwerten, die während der Wiedergabe gemeldet werden. Verwenden Sie sie zusammen mit der Metrik [Inhaltssegmentansichten](/help/reporting/metrics/content-segment-views.md) um zu analysieren, welche Teile von langformatigen Inhalts-Viewern tatsächlich genutzt werden.

## So wird diese Dimension ausgefüllt

Das Inhaltssegment wird vom Medien-Backend aus den Abspielkopfwerten berechnet, die in den Ereignissen der Sitzung gemeldet werden. Sie wird nicht vom Client festgelegt. Der angezeigte Wert wird von den Abspielkopfwerten abgeleitet, die während der Wiedergabe gesehen wurden.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.segment`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>Wenn der Abspielkopf während der Sitzung nicht korrekt gemeldet wird, kann das berechnete Segment ungenau sein. Bei Live-Streams wird das Segment aus den relativen Abspielkopfwerten berechnet, die während der Sitzung angezeigt werden.

## Dimensionselemente

Jedes Element ist ein Zeichenfolgenbereich, der die während einer Sitzung angezeigten Abspielkopfwerte abdeckt (z. B. `[0-5]`, `[5-10]`, `[10-15]`). Die Granularität ist auf fünf Minuten festgelegt.
