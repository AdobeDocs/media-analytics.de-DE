---
title: Netzwerk
description: Meldet das Broadcast-Netzwerk oder den Kanalnamen.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 9%

---


# Netzwerk

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Netzwerk**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/network.md) unter „Netzwerk“*

>[!ENDSHADEBOX]

Die Dimension **Netzwerk** zeigt den Broadcast-Netzwerk- oder Kanalnamen an (z. B. `"Fox"` oder `"ESPN"`). Verwenden Sie diese Option, um die Interaktion zwischen Netzwerken innerhalb derselben Streaming-Eigenschaft zu vergleichen.

## So wird diese Dimension ausgefüllt

Das Netzwerk wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.network`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videonetwork, post_videonetwork` |

## Dimensionselemente

Jedes Element ist der bei Sitzungsbeginn gemeldete Netzwerkwert. Verwenden Sie einen stabilen, eindeutigen Namen pro Netzwerk, damit die Daten nicht über Schreibvarianten hinweg fragmentiert werden.
