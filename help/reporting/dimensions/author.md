---
title: Autor
description: Gibt den Autor des Inhalts an. Wird hauptsächlich für Hörbücher verwendet.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 10%

---


# Autor

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Autor**behandelt. Unter [Autor](/help/implementation/variables/standard-metadata/author.md) finden Sie Informationen zum Erfassen dieser Variablen.*

>[!ENDSHADEBOX]

Die Dimension **Autor** zeigt den Autor des Inhalts an (z. B. `"Eleanor Clementine"`). Wird hauptsächlich für Hörbücher verwendet, gilt aber auch für Podcasts, deren Moderator oder Produzent die jeweilige Attribution ist.

## So wird diese Dimension ausgefüllt

Der Autor wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.author`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudioauthor` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsbeginn gemeldete literale Autorenname.
