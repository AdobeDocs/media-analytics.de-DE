---
title: Netzwerk
description: Meldet das Broadcast-Netzwerk oder den Kanalnamen.
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
source-wordcount: '127'
ht-degree: 12%
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.network`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## Dimensionselemente

Jedes Element ist der bei Sitzungsbeginn gemeldete Netzwerkwert. Verwenden Sie einen stabilen, eindeutigen Namen pro Netzwerk, damit die Daten nicht über Schreibvarianten hinweg fragmentiert werden.
