---
title: Sendungstyp
description: Gibt das Inhaltsformat an (vollständige Folge, Vorschau, Clip oder andere).
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
