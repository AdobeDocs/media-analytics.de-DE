---
title: Inhaltskanal
description: Gibt die Verteilungsstation, das Netzwerk oder die Eigenschaft an, an der die jeweilige Sitzung wiedergegeben wurde.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 7%

---


# Inhaltskanal

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Inhaltskanal**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/content-channel.md) unter „Inhaltskanal“*

>[!ENDSHADEBOX]

Die Dimension **Inhaltskanal** zeigt die Verteilungs-Workstation, das Netzwerk oder die Eigenschaft an, an der bzw. der jede Sitzung wiedergegeben wurde. Verwenden Sie diese Option, um die Wiedergabe nach Netzwerk oder Abschnitten einer Eigenschaft aufzuschlüsseln.

## So wird diese Dimension ausgefüllt

Der Kanal wird vom Player beim Sitzungsstart festgelegt und bleibt für die Dauer der Sitzung bestehen.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.channel`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Wenn der Kanal nicht festgelegt ist, wird die Dimension für diese Sitzung nicht ausgefüllt.

## Dimensionselemente

Jedes Element ist die literale Zeichenfolge, die beim Sitzungsbeginn festgelegt wird. Jede Zeichenfolge wird akzeptiert. Typische Werte sind ein Netzwerkname, ein Teil eines Site-Pfads oder eine interne Eigenschaftskennung.
