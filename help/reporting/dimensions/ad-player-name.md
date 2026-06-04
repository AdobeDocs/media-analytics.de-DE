---
title: Player-Namen hinzufügen
description: Gibt an, welcher Player jede Anzeige gerendert hat.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# Player-Namen hinzufügen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeigenplayer-Name**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/ads/ad-player-name.md) unter „Player-Name hinzufügen“*

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

Jedes Element ist der literale Anzeigenplayer-Name, der beim Anzeigenstart [ wird](/help/implementation/events/ads/ad-start.md).
