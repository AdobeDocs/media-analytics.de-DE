---
title: Anzeigenname
description: Meldet den für Menschen lesbaren Titel jeder Anzeige.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 6%

---


# Anzeigenname

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Berichtsdimension **Anzeigename**. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/ads/ad-name.md) unter „Anzeigename“*

>[!ENDSHADEBOX]

Die Dimension **Anzeigename** zeigt den für Menschen lesbaren Titel jeder Anzeige an.

## So wird diese Dimension ausgefüllt

Der Anzeigenname wird vom Player bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.ad.friendlyName`, wenn [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Daten-Feeds | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

In Adobe Analytics wird diese Dimension auf zwei Arten angezeigt: als **Anzeigename (Variable)** (direkt aus `a.media.ad.friendlyName` erfasst) und als **Anzeigename** (eine Klassifizierung, die von der [Ad](ad.md)-Dimension abgeleitet ist). Wenn Sie die Klassifizierung verwenden, sind Sie dafür verantwortlich, die Werte mithilfe von „Klassifizierungssätze[ aufzufüllen und ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). Die Verwendung von **Anzeigename (Variable)** erfordert keine Klassifizierungs-Pflege, aber Sie verlieren die garantierte 1::1-Beziehung zwischen dem Anzeigenamen und der übergeordneten Dimension [Anzeige](ad.md). Verwenden Sie die Komponente, die Ihr Implementierungs-Workflow am besten unterstützt.

## Dimensionselemente

Jedes Element ist der literale Anzeigentitel, der beim [Anzeigenstart“ angezeigt ](/help/implementation/events/ads/ad-start.md) (z. B. `"Ford F-150"`).
