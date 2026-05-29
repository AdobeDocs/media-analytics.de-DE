---
title: Album
description: Gibt das Album an, zu dem die Audiospur gehört.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.album`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## Dimensionselemente

Jedes Element ist der literale Albumtitel, der am Sitzungsbeginn gemeldet wird. Zwei Alben mit demselben Titel von verschiedenen Künstlern reduzieren sich zu einem einzigen Zeileneintrag. Paaren Sie mit der [Künstler](artist.md)-Dimension, um sie zu unterteilen.
