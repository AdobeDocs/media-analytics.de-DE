---
title: Anzeigenposition im Pod
description: Meldet die nullindizierte Position jeder Anzeige innerhalb ihrer übergeordneten Anzeigenunterbrechung.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 6%

---


# Anzeigenposition im Pod

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeige in Pod-Position**behandelt. Informationen [ Erfassen dieser Variablen finden Sie ](/help/implementation/variables/ads/ad-in-pod-position.md) „Anzeige in Pod-Position“*

>[!ENDSHADEBOX]

Die Dimension **Anzeige in Pod** zeigt die nullindizierte Position jeder Anzeige innerhalb der übergeordneten Anzeigenunterbrechung an. Die erste Anzeige in einem Pod ist `0`, die zweite `1` und so weiter. Verwenden Sie die Dimension, um Interaktion und Abschluss nach Position innerhalb einer Werbeunterbrechung zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Position der Anzeige wird vom Player bei jedem `media.adStart` festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.podPosition`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadinpod, post_videoadinpod` |

## Dimensionselemente

Jedes Element ist der Ganzzahlpositionswert (`0`, `1`, `2`, …) Meldung am `media.adStart`.
