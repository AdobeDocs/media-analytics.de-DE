---
title: Folge
description: Meldet die Nummer der Folge innerhalb einer Staffel.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 12%
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsbeginn gemeldete literale Episodenwert (in der Regel eine ganze Zeichenfolge wie `"13"`). Die Episodennummern allein sind über die Staffeln hinweg nicht eindeutig; paaren Sie sich mit Staffel für eindeutige Breakouts.
