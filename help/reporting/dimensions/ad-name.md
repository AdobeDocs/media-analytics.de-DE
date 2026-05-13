---
title: Anzeigenname
description: Meldet den für Menschen lesbaren Titel jeder Anzeige.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---


# Anzeigenname

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Berichtsdimension **Anzeigename**. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/ads/ad-name.md) unter „Anzeigename“*

>[!ENDSHADEBOX]

Die Dimension **Anzeigename** zeigt den für Menschen lesbaren Titel jeder Anzeige an.

## So wird diese Dimension ausgefüllt

Der Anzeigenname wird vom Player bei jedem `media.adStart` festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.friendlyName`, wenn [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadname, post_videoadname` |

In Adobe Analytics wird diese Dimension auf zwei Arten angezeigt: als **Anzeigename (Variable)** (direkt aus `a.media.ad.friendlyName` erfasst) und als **Anzeigename** (eine Klassifizierung, die von der [Ad](ad.md)-Dimension abgeleitet ist). Wenn Sie die Klassifizierung verwenden, sind Sie dafür verantwortlich, die Werte mithilfe von „Klassifizierungssätze[&#x200B; aufzufüllen und &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). Die Verwendung von **Anzeigename (Variable)** erfordert keine Klassifizierungs-Pflege, aber Sie verlieren die garantierte 1::1-Beziehung zwischen dem Anzeigenamen und der übergeordneten Dimension [Anzeige](ad.md). Verwenden Sie die Komponente, die Ihr Implementierungs-Workflow am besten unterstützt.

## Dimensionselemente

Jedes Element ist der literale Anzeigentitel, der für `media.adStart` gemeldet wird (z. B. `"Ford F-150"`).
