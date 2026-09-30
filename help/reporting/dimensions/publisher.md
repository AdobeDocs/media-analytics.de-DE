---
title: Publisher
description: Gibt den Herausgeber des Audioinhalts an.
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
source-wordcount: '114'
ht-degree: 12%
---

# Publisher

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Publisher**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/publisher.md) unter „Publisher“*

>[!ENDSHADEBOX]

Die Dimension **Publisher** zeigt den Herausgeber des Audioinhalts an (z. B. ein Podcast-Netzwerk oder einen Hörbuchherausgeber). Verwenden Sie diese Option, um die Interaktion zwischen Herausgebern in einem kuratierten Audiokatalog zu vergleichen.

## So wird diese Dimension ausgefüllt

Der Publisher wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.publisher`, wenn [[!UICONTROL Audio-]](/help/reporting/setup/analytics-reporting.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsstart gemeldete literale Herausgebername.
