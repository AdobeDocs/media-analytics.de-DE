---
title: Anzeigenposition im Pod
description: Meldet die nullindizierte Position jeder Anzeige innerhalb ihrer übergeordneten Anzeigenunterbrechung.
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
source-wordcount: '156'
ht-degree: 8%
---

# Anzeigenposition im Pod

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeige in Pod-Position**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden Sie &#x200B;](/help/implementation/variables/ads/ad-in-pod-position.md) „Anzeige in Pod-Position“*

>[!ENDSHADEBOX]

Die Dimension **Anzeige in Pod** zeigt die nullindizierte Position jeder Anzeige innerhalb der übergeordneten Anzeigenunterbrechung an. Die erste Anzeige in einem Pod ist `0`, die zweite `1` und so weiter. Verwenden Sie die Dimension, um Interaktion und Abschluss nach Position innerhalb einer Werbeunterbrechung zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Position der Anzeige im Pod wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md) festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.podPosition`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## Dimensionselemente

Jedes Element ist der Ganzzahlpositionswert (`0`, `1`, `2`, …) Meldung zu [Anzeigenstart](/help/implementation/events/ads/ad-start.md).
