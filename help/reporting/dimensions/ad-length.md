---
title: Anzeigenlänge
description: Gibt die Dauer jeder Anzeige in Sekunden an.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# Anzeigenlänge

>[!BEGINSHADEBOX]

*Diese Seite deckt die Berichtsdimension **Anzeigenlänge**&#x200B;ab. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/ad-length.md) unter „Anzeigenlänge“*

>[!ENDSHADEBOX]

Die Dimension **Anzeigenlänge** zeigt die Dauer jeder Anzeige in Sekunden an.

## So wird diese Dimension ausgefüllt

Die Anzeigenlänge wird vom Player bei jedem `media.adStart` festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.length`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadlength, post_videoadlength` |

In Adobe Analytics wird diese Dimension auf zwei Arten angezeigt: als **Anzeigenlänge (variabel)** (direkt aus `a.media.ad.length` erfasst) und als **Anzeigenlänge** (eine Klassifizierung, die von der Dimension [Anzeige](ad.md) abgeleitet wird). Wenn Sie die Klassifizierung verwenden, sind Sie dafür verantwortlich, die Werte mithilfe von „Klassifizierungssätze[&#x200B; aufzufüllen und &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). Die Verwendung von **Anzeigenlänge (Variable)** erfordert keine Classification-Wartung, aber Sie verlieren die garantierte 1::1-Beziehung zwischen der Anzeigenlänge und der übergeordneten Dimension [Anzeige](ad.md). Verwenden Sie die Komponente, die Ihr Implementierungs-Workflow am besten unterstützt.

## Dimensionselemente

Jedes Element ist der literale Anzeigenlängenwert in Sekunden, der für `media.adStart` gemeldet wird.
