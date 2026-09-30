---
title: Anzeigenladevorgänge
description: Gibt die Art der Anzeigenauslastung an, die für jede Streaming-Mediensitzung verwendet wird.
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
source-wordcount: '161'
ht-degree: 8%
---

# Anzeigenladevorgänge

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Anzeigenladevorgänge**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/ad-load-type.md) unter „Anzeigenladungstyp“*

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
