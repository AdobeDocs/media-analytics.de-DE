---
title: Inhaltsname
description: Gibt den für Menschen lesbaren Titel jeder Mediensitzung an.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 10%

---


# Inhaltsname

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Inhaltsname**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/content-name.md) unter „Inhaltsname“*

>[!ENDSHADEBOX]

Die Dimension **Inhaltsname** zeigt den für Menschen lesbaren Titel jeder Mediensitzung an.

## So wird diese Dimension ausgefüllt

Der Anzeigename wird vom Player beim Sitzungsstart festgelegt. Der gemeldete Wert entspricht dem gesendeten Wert.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.friendlyName`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
