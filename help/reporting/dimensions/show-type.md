---
title: Sendungstyp
description: Gibt das Inhaltsformat an (vollständige Folge, Vorschau, Clip oder andere).
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
source-wordcount: '145'
ht-degree: 11%
---

# Sendungstyp

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Typ anzeigen**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden Sie &#x200B;](/help/implementation/variables/standard-metadata/show-type.md) „Anzeigen-Typ“*

>[!ENDSHADEBOX]

Die Dimension **Typ anzeigen** zeigt das Inhaltsformat mit einem Zeichenfolgen-Ganzzahlcode an. Verwenden Sie diese Option, um bei der Messung der Interaktion die Anzeige eines vollständigen Programms von kurzen Inhalten wie Trailern und Clips zu trennen.

## So wird diese Dimension ausgefüllt

Der Sendungstyp wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.type`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## Dimensionselemente

| Wert | Beschreibung |
| --- | --- |
| `0` | Vollständige Folge |
| `1` | Vorschau für Trailer |
| `2` | Clip |
| `3` | Sonstige |

Die Werte werden als Zeichenfolgen gemeldet. Benutzerdefinierte Werte werden akzeptiert, aber nicht in die vier integrierten Behälter hochgerechnet.
