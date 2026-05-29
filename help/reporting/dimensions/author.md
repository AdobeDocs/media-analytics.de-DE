---
title: Autor
description: Gibt den Autor des Inhalts an. Wird hauptsächlich für Hörbücher verwendet.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 11%

---


# Autor

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Autor**&#x200B;behandelt. Unter [Autor](/help/implementation/variables/standard-metadata/author.md) finden Sie Informationen zum Erfassen dieser Variablen.*

>[!ENDSHADEBOX]

Die Dimension **Autor** zeigt den Autor des Inhalts an (z. B. `"Eleanor Clementine"`). Wird hauptsächlich für Hörbücher verwendet, gilt aber auch für Podcasts, deren Moderator oder Produzent die jeweilige Attribution ist.

## So wird diese Dimension ausgefüllt

Der Autor wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.author`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsbeginn gemeldete literale Autorenname.
