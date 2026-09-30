---
title: Künstler
description: Gibt den Interpreten für Audioinhalte an.
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
source-wordcount: '128'
ht-degree: 10%
---

# Künstler

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Interpret**behandelt. Unter [Interpret](/help/implementation/variables/standard-metadata/artist.md) finden Sie Informationen zum Erfassen dieser Variablen.*

>[!ENDSHADEBOX]

Die Dimension **Interpret** zeigt den Interpreten für Audioinhalte an (z. B. `"Crested Larks"`). Hiermit können Sie die Interaktion mit Musik- oder Podcast-Katalogen nach Darsteller unterbinden.

## So wird diese Dimension ausgefüllt

Der Interpret wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.artist`, wenn [[!UICONTROL Audio-]](/help/reporting/setup/analytics-reporting.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudioartist` |
| Audience Manager | `c_contextdata.a.media.artist` |

## Dimensionselemente

Bei jedem Element handelt es sich um den beim Sitzungsbeginn gemeldeten literalen Künstlernamen. Verwenden Sie für jeden Interpreten einen stabilen, kanonischen Namen, damit die Daten nicht über Formatierungsvarianten hinweg fragmentiert werden.
