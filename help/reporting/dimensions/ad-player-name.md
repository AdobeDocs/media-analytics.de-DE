---
title: Player-Namen hinzufügen
description: Gibt an, welcher Player jede Anzeige gerendert hat.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.playerName`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## Dimensionselemente

Jedes Element ist der literale Anzeigenplayer-Name, der beim Anzeigenstart [&#x200B; wird](/help/implementation/events/ads/ad-start.md).
