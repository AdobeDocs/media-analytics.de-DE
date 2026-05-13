---
title: MVPD
description: Gibt den Kabel-, Satelliten- oder virtuellen Provider an, über den sich der Benutzer authentifiziert hat.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 8%

---


# MVPD

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **MVPD**behandelt. Informationen ](/help/implementation/variables/standard-metadata/mvpd.md) Erfassen dieser Variablen finden Sie unter [MVPD*

>[!ENDSHADEBOX]

Die Dimension **MVPD** (Multi-Channel Video Programming Distributor) zeigt den Anbieter an, über den sich der Benutzer über Adobe Pass authentifiziert hat (z. B. `"Comcast"` oder `"DirecTV"`). Verwenden Sie diese Option, um die Interaktion des Authentifizierungsanbieters aufzuheben.

## So wird diese Dimension ausgefüllt

MVPD wird vom Player beim Sitzungsstart festgelegt, wenn der Inhalt hinter Adobe Pass gated wird.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pass.mvpd`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videomvpd, post_videomvpd` |

## Dimensionselemente

Jedes Element ist der wörtliche MVPD-Name, der beim Sitzungsstart gemeldet wird. Verwenden Sie die kanonische Adobe Pass MVPD-Kennung pro Provider, sodass die Daten pro Provider zu einem einzigen Zeileneintrag aggregiert werden.
