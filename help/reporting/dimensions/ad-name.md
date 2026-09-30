---
title: Anzeigenname
description: Meldet den für Menschen lesbaren Titel jeder Anzeige.
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
source-wordcount: '194'
ht-degree: 7%
---

# Anzeigenname

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Berichtsdimension **Anzeigename**. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/ad-name.md) unter „Anzeigename“*

>[!ENDSHADEBOX]

Die Dimension **Anzeigename** zeigt den für Menschen lesbaren Titel jeder Anzeige an.

## So wird diese Dimension ausgefüllt

Der Anzeigenname wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.friendlyName`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

In Adobe Analytics wird diese Dimension auf zwei Arten angezeigt: als **Anzeigename (Variable)** (direkt aus `a.media.ad.friendlyName` erfasst) und als **Anzeigename** (eine Klassifizierung, die von der [Ad](ad.md)-Dimension abgeleitet ist). Wenn Sie die Klassifizierung verwenden, sind Sie dafür verantwortlich, die Werte mithilfe von „Klassifizierungssätze[&#x200B; aufzufüllen und &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). Die Verwendung von **Anzeigename (Variable)** erfordert keine Klassifizierungs-Pflege, aber Sie verlieren die garantierte 1:1-Beziehung zwischen dem Anzeigenamen und der übergeordneten Dimension [Anzeige](ad.md). Verwenden Sie die Komponente, die Ihr Implementierungs-Workflow am besten unterstützt.

## Dimensionselemente

Jedes Element ist der literale Anzeigentitel, der beim [Anzeigenstart“ angezeigt &#x200B;](/help/implementation/events/ads/ad-start.md) (z. B. `"Ford F-150"`).
