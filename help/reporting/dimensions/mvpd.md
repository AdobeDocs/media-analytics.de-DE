---
title: MVPD
description: Gibt den Kabel-, Satelliten- oder virtuellen Provider an, über den sich der Benutzer authentifiziert hat.
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
source-wordcount: '150'
ht-degree: 10%
---

# MVPD

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **MVPD**&#x200B;behandelt. Informationen [&#128279;](/help/implementation/variables/standard-metadata/mvpd.md) Erfassen dieser Variablen finden Sie unter MVPD*

>[!ENDSHADEBOX]

Die Dimension **MVPD** (Multi-Channel Video Programming Distributor) zeigt den Anbieter an, über den sich der Benutzer über Adobe Pass authentifiziert hat (z. B. `"Comcast"` oder `"DirecTV"`). Verwenden Sie diese Option, um die Interaktion des Authentifizierungsanbieters aufzuheben.

## So wird diese Dimension ausgefüllt

MVPD wird vom Player beim Sitzungsstart festgelegt, wenn der Inhalt hinter Adobe Pass gated wird.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pass.mvpd`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## Dimensionselemente

Jedes Element ist der wörtliche MVPD-Name, der beim Sitzungsstart gemeldet wird. Verwenden Sie die kanonische Adobe Pass MVPD-Kennung pro Provider, sodass die Daten pro Provider zu einem einzigen Zeileneintrag aggregiert werden.
