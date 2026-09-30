---
title: Zeit bis zum Start (Dimension)
description: Gibt die Zeit an, die vor dem ersten gerenderten Frame verstrichen ist.
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
source-wordcount: '190'
ht-degree: 7%
---

# Zeit bis zum Start (Dimension)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Dimension **Zeit bis zum Start**behandelt. Adobe Analytics füllt automatisch eine paarweise [Time to Start (Metrik](/help/reporting/metrics/time-to-start.md) aus derselben `a.media.qoe.timeToStart` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.timeToStart` bereit, das Sie als Dimension oder Metrik verwenden können. Informationen [ Erfassen dieser Variablen finden Sie ](/help/implementation/variables/quality/time-to-start.md) „Zeit bis zum Start“*

>[!ENDSHADEBOX]

Die Dimension **Zeit bis**&quot; zeigt die Zeit zwischen dem Sitzungsstart und dem ersten Frame-Rendering an. Verwenden Sie die Dimension, um die Interaktion nach Startzeit-Bucket aufzuheben. Adobe speichert den Wert in Sekunden und konvertiert bei der Aufnahme die Millisekunden, die der Player meldet.

## So wird diese Dimension ausgefüllt

Der Player legt `timeToStart` auf das QoE-Objekt fest, bevor der Sitzungsstart ausgelöst wird. Das Backend meldet den Wert beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.timeToStart`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## Dimensionselemente

Jedes Element ist der beim Schließen-Aufruf gemeldete literale Wert der Startzeit.
