---
title: Station
description: Gibt den Namen oder die ID des Radiosenders für den Audio-Broadcast-Inhalt an.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# Station

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Station**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/station.md) unter „Station“*

>[!ENDSHADEBOX]

Die Dimension **Station** zeigt den Namen oder die ID der Radiostation an, von der der Audioinhalt übertragen wird (z. B. `"NPR"` oder `"WXYZ-FM"`). Verwendet, um die Interaktion zwischen Stationen in einem syndizierten Netzwerk zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Station wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.station`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Dimensionselemente

Jedes Element ist der eigentliche Stationsname oder die ID, die beim Sitzungsstart gemeldet wird. Verwenden Sie für jede Station eine einzelne kanonische Kennung, damit die Interaktion nicht über Rufzeichenvarianten hinweg fragmentiert wird.
