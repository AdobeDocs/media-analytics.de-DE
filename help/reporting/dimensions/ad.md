---
title: Anzeige
description: Meldet jede abgespielte eindeutige Anzeige, verschlüsselt durch die Werbe-ID.
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
source-wordcount: '188'
ht-degree: 8%
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.name`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. bleibt für die Dauer des Besuchs erhalten. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>Werbe-ID ist erforderlich. Wenn sie nicht festgelegt oder leer ist, wird die Anzeige aus dem Streaming-Medien-Anzeigenbericht gelöscht.

## Dimensionselemente

Jedes Element ist eine eindeutige Werbe-ID, die beim [Anzeigenstart](/help/implementation/events/ads/ad-start.md) gemeldet wird. Verwenden Sie eine stabile Kennung pro Kreativschaffender, damit dieselbe Anzeige sitzungsübergreifend für ein einzelnes Zeilenelement verwendet wird.
