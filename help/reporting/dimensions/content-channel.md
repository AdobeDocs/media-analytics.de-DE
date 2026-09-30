---
title: Inhaltskanal
description: Gibt die Verteilungsstation, das Netzwerk oder die Eigenschaft an, an der die jeweilige Sitzung wiedergegeben wurde.
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
source-wordcount: '163'
ht-degree: 8%
---

# Inhaltskanal

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Inhaltskanal**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/core/content-channel.md) unter „Inhaltskanal“*

>[!ENDSHADEBOX]

Die Dimension **Inhaltskanal** zeigt die Verteilungs-Workstation, das Netzwerk oder die Eigenschaft an, an der bzw. der jede Sitzung wiedergegeben wurde. Verwenden Sie diese Option, um die Wiedergabe nach Netzwerk oder Abschnitten einer Eigenschaft aufzuschlüsseln.

## So wird diese Dimension ausgefüllt

Der Kanal wird vom Player beim Sitzungsstart festgelegt und bleibt für die Dauer der Sitzung bestehen.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.channel`, wenn [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Wenn der Kanal nicht festgelegt ist, wird die Dimension für diese Sitzung nicht ausgefüllt.

## Dimensionselemente

Jedes Element ist die literale Zeichenfolge, die beim Sitzungsbeginn festgelegt wird. Jede Zeichenfolge wird akzeptiert. Typische Werte sind ein Netzwerkname, ein Teil eines Site-Pfads oder eine interne Eigenschaftskennung.
