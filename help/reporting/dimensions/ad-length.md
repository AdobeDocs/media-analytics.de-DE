---
title: Anzeigenlänge
description: Gibt die Dauer jeder Anzeige in Sekunden an.
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
source-wordcount: '195'
ht-degree: 7%
---

# Anzeigenlänge

>[!BEGINSHADEBOX]

*Diese Seite deckt die Berichtsdimension **Anzeigenlänge**ab. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/ads/ad-length.md) unter „Anzeigenlänge“*

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

In Adobe Analytics wird diese Dimension auf zwei Arten angezeigt: als **Anzeigenlänge (variabel)** (direkt aus `a.media.ad.length` erfasst) und als **Anzeigenlänge** (eine Klassifizierung, die von der Dimension [Anzeige](ad.md) abgeleitet wird). Wenn Sie die Klassifizierung verwenden, sind Sie dafür verantwortlich, die Werte mithilfe von „Klassifizierungssätze[ aufzufüllen und ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). Die Verwendung von **Anzeigenlänge (Variable)** erfordert keine Classification-Wartung, aber Sie verlieren die garantierte 1:1-Beziehung zwischen der Anzeigenlänge und der übergeordneten Dimension [Anzeige](ad.md). Verwenden Sie die Komponente, die Ihr Implementierungs-Workflow am besten unterstützt.

## Dimensionselemente

Jedes Element ist der literale Wert der Anzeigenlänge in Sekunden, der beim Anzeigen-Start [ wird](/help/implementation/events/ads/ad-start.md).
