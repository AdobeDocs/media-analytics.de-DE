---
title: Folge
description: Meldet die Nummer der Folge innerhalb einer Staffel.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 9%

---


# Folge

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Reporting **Dimension &quot;**&quot; behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/episode.md) unter „Episode“*

>[!ENDSHADEBOX]

Die Dimension **Folge** zeigt die Nummer der Folge innerhalb einer Staffel an. Verwenden Sie sie zusammen mit [](show.md) und [Staffel](season.md), um die Interaktion auf der Ebene der einzelnen Episoden zu unterbrechen.

## So wird diese Dimension ausgefüllt

Die Folge wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.episode`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoepisode, post_videoepisode` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsbeginn gemeldete literale Episodenwert (in der Regel eine ganze Zeichenfolge wie `"13"`). Die Episodennummern allein sind über die Staffeln hinweg nicht eindeutig; paaren Sie sich mit Staffel für eindeutige Breakouts.
