---
title: Künstler
description: Gibt den Interpreten für Audioinhalte an.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 10%

---


# Künstler

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Interpret**&#x200B;behandelt. Unter [Interpret](/help/implementation/variables/standard-metadata/artist.md) finden Sie Informationen zum Erfassen dieser Variablen.*

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
