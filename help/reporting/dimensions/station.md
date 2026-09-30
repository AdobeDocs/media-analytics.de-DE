---
title: Station
description: Gibt den Namen oder die ID des Radiosenders für den Audio-Broadcast-Inhalt an.
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.station`, wenn [[!UICONTROL Audio-]](/help/reporting/setup/analytics-reporting.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Dimensionselemente

Jedes Element ist der eigentliche Stationsname oder die ID, die beim Sitzungsstart gemeldet wird. Verwenden Sie für jede Station eine einzelne kanonische Kennung, damit die Interaktion nicht über Rufzeichenvarianten hinweg fragmentiert wird.
