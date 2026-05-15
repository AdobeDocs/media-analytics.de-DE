---
title: Serie
description: Gibt den Programm- oder Seriennamen für Videoinhalte an, die Teil einer Serie sind.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.show`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Dimensionselemente

Jedes Element ist der wörtliche Sendungsname, der beim Sitzungsstart gemeldet wird (z. B. `"Blinding Light"`). Verwenden Sie stabile, eindeutige Namen pro Sendung, damit Daten nicht über nicht verwandte Programme hinweg reduziert werden, die ein Wort gemeinsam haben.
