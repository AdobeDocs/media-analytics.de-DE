---
title: Folge
description: Meldet die Nummer der Folge innerhalb einer Staffel.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 10%

---


# Folge

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting **Dimension &quot;**&quot; behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/episode.md) unter „Episode“*

>[!ENDSHADEBOX]

Die Dimension **Folge** zeigt die Nummer der Folge innerhalb einer Staffel an. Verwenden Sie sie zusammen mit [&#128279;](show.md) und [Staffel](season.md), um die Interaktion auf der Ebene der einzelnen Episoden zu unterbrechen.

## So wird diese Dimension ausgefüllt

Die Folge wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.episode`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsbeginn gemeldete literale Episodenwert (in der Regel eine ganze Zeichenfolge wie `"13"`). Die Episodennummern allein sind über die Staffeln hinweg nicht eindeutig; paaren Sie sich mit Staffel für eindeutige Breakouts.
