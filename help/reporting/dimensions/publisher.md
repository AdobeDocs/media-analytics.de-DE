---
title: Publisher
description: Gibt den Herausgeber des Audioinhalts an.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.publisher`, wenn [[!UICONTROL Audio-]](/help/reporting/setup/analytics-reporting.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsstart gemeldete literale Herausgebername.
