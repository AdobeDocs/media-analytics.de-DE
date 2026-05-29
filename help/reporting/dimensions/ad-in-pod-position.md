---
title: Anzeigenposition im Pod
description: Meldet die nullindizierte Position jeder Anzeige innerhalb ihrer übergeordneten Anzeigenunterbrechung.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 7%

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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.podPosition`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## Dimensionselemente

Jedes Element ist der Ganzzahlpositionswert (`0`, `1`, `2`, …) Meldung zu [Anzeigenstart](/help/implementation/events/ads/ad-start.md).
