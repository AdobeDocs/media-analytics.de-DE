---
title: Publisher
description: Gibt den Herausgeber des Audioinhalts an.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 10%

---


# Publisher

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Publisher**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/publisher.md) unter „Publisher“*

>[!ENDSHADEBOX]

Die Dimension **Publisher** zeigt den Herausgeber des Audioinhalts an (z. B. ein Podcast-Netzwerk oder einen Hörbuchherausgeber). Verwenden Sie diese Option, um die Interaktion zwischen Herausgebern in einem kuratierten Audiokatalog zu vergleichen.

## So wird diese Dimension ausgefüllt

Der Publisher wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.publisher`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiopublisher` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsstart gemeldete literale Herausgebername.
