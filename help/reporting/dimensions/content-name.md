---
title: Inhaltsname
description: Gibt den für Menschen lesbaren Titel jeder Mediensitzung an.
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
source-wordcount: '162'
ht-degree: 11%
---

# Inhaltsname

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Inhaltsname**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/core/content-name.md) unter „Inhaltsname“*

>[!ENDSHADEBOX]

Die Dimension **Inhaltsname** zeigt den für Menschen lesbaren Titel jeder Mediensitzung an.

## So wird diese Dimension ausgefüllt

Der Anzeigename wird vom Player beim Sitzungsstart festgelegt. Der gemeldete Wert entspricht dem gesendeten Wert.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.friendlyName`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>In Adobe Analytics entspricht dieser Wert auch einer Klassifizierung **Videoname** in der Dimension [Inhalt](content.md). Sie sind dafür verantwortlich, diese Klassifizierung separat auszufüllen und zu pflegen. Customer Journey Analytics verwendet diese Dimension direkt.

>[!IMPORTANT]
>
>Wenn der Inhaltsname nicht festgelegt ist, wird die Dimension für diese Sitzung nicht ausgefüllt.

## Dimensionselemente

Jedes Element ist der beim Sitzungsstart angezeigte wörtliche Titel (z. B. `"Blinding Light"`).
