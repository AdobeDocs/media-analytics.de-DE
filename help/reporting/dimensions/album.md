---
title: Album
description: Gibt das Album an, zu dem die Audiospur gehört.
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
source-wordcount: '136'
ht-degree: 10%
---

# Album

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Album**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/album.md) unter „Album“*

>[!ENDSHADEBOX]

Die Dimension **Album** gibt das Album an, zu dem die Audiospur gehört (z. B. `"Pinegrove"`). Verwenden Sie diese Option, um die Interaktion auf allen Titeln desselben Albums zu aggregieren.

## So wird diese Dimension ausgefüllt

Das Album wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.album`, wenn [[!UICONTROL Audio-]](/help/reporting/setup/analytics-reporting.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## Dimensionselemente

Jedes Element ist der literale Albumtitel, der am Sitzungsbeginn gemeldet wird. Zwei Alben mit demselben Titel von verschiedenen Künstlern reduzieren sich zu einem einzigen Zeileneintrag. Paaren Sie mit der [Künstler](artist.md)-Dimension, um sie zu unterteilen.
