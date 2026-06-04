---
title: Netzwerk
description: Meldet das Broadcast-Netzwerk oder den Kanalnamen.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 11%

---


# Netzwerk

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Netzwerk**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/network.md) unter „Netzwerk“*

>[!ENDSHADEBOX]

Die Dimension **Netzwerk** zeigt den Broadcast-Netzwerk- oder Kanalnamen an (z. B. `"Fox"` oder `"ESPN"`). Verwenden Sie diese Option, um die Interaktion zwischen Netzwerken innerhalb derselben Streaming-Eigenschaft zu vergleichen.

## So wird diese Dimension ausgefüllt

Das Netzwerk wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.network`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## Dimensionselemente

Jedes Element ist der bei Sitzungsbeginn gemeldete Netzwerkwert. Verwenden Sie einen stabilen, eindeutigen Namen pro Netzwerk, damit die Daten nicht über Schreibvarianten hinweg fragmentiert werden.
