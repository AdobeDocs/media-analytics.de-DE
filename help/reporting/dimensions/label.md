---
title: Beschriftung
description: Meldet das Plattenlabel, unter dem der Audioinhalt freigegeben wurde.
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
source-wordcount: '134'
ht-degree: 10%
---

# Beschriftung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Beschriftung**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/label.md) unter „Bezeichnung“*

>[!ENDSHADEBOX]

Die **label**-Dimension zeigt die Plattenfirma an, die den Audioinhalt freigegeben hat (z. B. `"Capitol Records"`). Verwenden Sie diese Option, um die Interaktion zwischen Labels in einem Musik- oder Podcast-Katalog zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Beschriftung wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.label`, wenn [[!UICONTROL Audio-]](/help/reporting/setup/analytics-reporting.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## Dimensionselemente

Jedes Element ist der literale Bezeichnungsname, der beim Sitzungsstart gemeldet wird. Verwenden Sie für jedes Label einen stabilen, kanonischen Namen, damit die Interaktion nicht über Rechtschreib- oder Aufdruckvarianten hinweg fragmentiert.
