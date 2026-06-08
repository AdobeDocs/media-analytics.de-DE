---
title: Anzeigenladevorgänge
description: Gibt die Art der Anzeigenauslastung an, die für jede Streaming-Mediensitzung verwendet wird.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# Anzeigenladevorgänge

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeigenladevorgänge**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/ad-load-type.md) unter „Anzeigenladungstyp“*

>[!ENDSHADEBOX]

Die Dimension **Anzeige lädt** zeigt den Typ der zu Beginn jeder Streaming-Mediensitzung geladenen Anzeige an. Der Wert ist kundendefiniert und ermöglicht es Unternehmen, Sitzungen anhand ihres Anzeigenbereitstellungsmechanismus (z. B. `"linear"`, `"dynamic"` oder `"programmatic"`) zu klassifizieren.

## So wird diese Dimension ausgefüllt

Der Anzeigenladungstyp wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.adLoad`, wenn [[!UICONTROL Streaming-]](/help/reporting/setup/analytics-reporting.md)) konfiguriert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## Dimensionselemente

Jedes Element ist die Zeichenfolge des Literal- und Ladetyps, die beim Sitzungsstart festgelegt wird. Die Werte sind nicht auf eine standardmäßige Auflistung beschränkt. Definieren Sie eine Taxonomie, die über Ihre Implementierungen hinweg konsistent ist, sodass sich Werte in Berichten vorhersehbar entwickeln.
