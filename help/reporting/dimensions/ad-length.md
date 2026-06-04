---
title: Anzeigenlänge
description: Gibt die Dauer jeder Anzeige in Sekunden an.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Anzeigenlänge

>[!BEGINSHADEBOX]

*Diese Seite deckt die Berichtsdimension **Anzeigenlänge**&#x200B;ab. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/ad-length.md) unter „Anzeigenlänge“*

>[!ENDSHADEBOX]

Die Dimension **Anzeigenlänge** zeigt die Dauer jeder Anzeige in Sekunden an.

## So wird diese Dimension ausgefüllt

Die Anzeigenlänge wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.length`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadlength`, `post_videoadlength` |
| Audience Manager | `c_contextdata.a.media.ad.length` |

In Adobe Analytics wird diese Dimension auf zwei Arten angezeigt: als **Anzeigenlänge (variabel)** (direkt aus `a.media.ad.length` erfasst) und als **Anzeigenlänge** (eine Klassifizierung, die von der Dimension [Anzeige](ad.md) abgeleitet wird). Wenn Sie die Klassifizierung verwenden, sind Sie dafür verantwortlich, die Werte mithilfe von „Klassifizierungssätze[&#x200B; aufzufüllen und &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). Die Verwendung von **Anzeigenlänge (Variable)** erfordert keine Classification-Wartung, aber Sie verlieren die garantierte 1::1-Beziehung zwischen der Anzeigenlänge und der übergeordneten Dimension [Anzeige](ad.md). Verwenden Sie die Komponente, die Ihr Implementierungs-Workflow am besten unterstützt.

## Dimensionselemente

Jedes Element ist der literale Wert der Anzeigenlänge in Sekunden, der beim Anzeigen-Start [&#x200B; wird](/help/implementation/events/ads/ad-start.md).
