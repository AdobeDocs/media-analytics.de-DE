---
title: Serie
description: Gibt den Programm- oder Seriennamen für Videoinhalte an, die Teil einer Serie sind.
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
source-wordcount: '158'
ht-degree: 10%
---

# Serie

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeigen**&#x200B;behandelt. Siehe [Anzeigen](/help/implementation/variables/standard-metadata/show.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Anzeigen** zeigt den Namen des Programms oder der Serie an. Folgen aus mehreren Staffeln werden zum selben Zeileneintrag der Sendung hochgerechnet. Verwenden Sie ihn also, um die Interaktion während des gesamten Lebenszyklus einer Serie zu vergleichen.

## So wird diese Dimension ausgefüllt

„Anzeigen“ wird vom Player beim Sitzungsstart festgelegt, wenn der Inhalt Teil einer Serie ist.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.show`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Dimensionselemente

Jedes Element ist der wörtliche Sendungsname, der beim Sitzungsstart gemeldet wird (z. B. `"Blinding Light"`). Verwenden Sie stabile, eindeutige Namen pro Sendung, damit Daten nicht über nicht verwandte Programme hinweg reduziert werden, die ein Wort gemeinsam haben.
