---
title: Autor
description: Gibt den Autor des Inhalts an. Wird hauptsächlich für Hörbücher verwendet.
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
source-wordcount: '119'
ht-degree: 11%
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.author`, wenn [[!UICONTROL Audio-]](/help/reporting/setup/analytics-reporting.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsbeginn gemeldete literale Autorenname.
