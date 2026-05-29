---
title: Anzeige
description: Meldet jede abgespielte eindeutige Anzeige, verschlüsselt durch die Werbe-ID.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 7%

---


# Anzeige

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeige**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/ad-id.md) unter „Anzeigen-ID“*

>[!ENDSHADEBOX]

Die Dimension **Anzeige** zeigt jede abgespielte eindeutige Anzeige an, die durch die beim Anzeigenstart festgelegte [-ID &#x200B;](/help/implementation/events/ads/ad-start.md) wird. Die Dimension ist die primäre Aufschlüsselung für das Anzeigen-Reporting und der Join-Schlüssel für Klassifizierungen auf Anzeigenebene wie Anzeigename, Anzeigenlänge und Creative-ID.

## So wird diese Dimension ausgefüllt

Die Anzeige wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis als stabile Kennung für die Anzeige festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.name`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. bleibt für die Dauer des Besuchs erhalten. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>Werbe-ID ist erforderlich. Wenn sie nicht festgelegt oder leer ist, wird die Anzeige aus dem Streaming-Medien-Anzeigenbericht gelöscht.

## Dimensionselemente

Jedes Element ist eine eindeutige Werbe-ID, die beim [Anzeigenstart](/help/implementation/events/ads/ad-start.md) gemeldet wird. Verwenden Sie eine stabile Kennung pro Kreativschaffender, damit dieselbe Anzeige sitzungsübergreifend für ein einzelnes Zeilenelement verwendet wird.
