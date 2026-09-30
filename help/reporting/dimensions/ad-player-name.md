---
title: Player-Namen hinzufügen
description: Gibt an, welcher Player jede Anzeige gerendert hat.
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
source-wordcount: '134'
ht-degree: 10%
---

# Player-Namen hinzufügen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeigenplayer-Name**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/ad-player-name.md) unter „Player-Name hinzufügen“*

>[!ENDSHADEBOX]

Die Dimension **Name des Anzeigen** gibt an, welcher Player jede Anzeige gerendert hat (z. B. `"Freewheel"`, `"Google IMA"`). Der Anzeigen-Player kann sich vom Hauptinhalt-Player unterscheiden, wenn Anzeigen von einem Server-seitigen Anzeigeneinfüge-Service zusammengefügt werden.

## So wird diese Dimension ausgefüllt

Der Name des Anzeigen-Players wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.playerName`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## Dimensionselemente

Jedes Element ist der literale Anzeigenplayer-Name, der beim Anzeigenstart [&#x200B; wird](/help/implementation/events/ads/ad-start.md).
