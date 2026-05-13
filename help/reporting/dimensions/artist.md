---
title: Künstler
description: Gibt den Interpreten für Audioinhalte an.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 9%

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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.artist`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudioartist` |

## Dimensionselemente

Bei jedem Element handelt es sich um den beim Sitzungsbeginn gemeldeten literalen Künstlernamen. Verwenden Sie für jeden Interpreten einen stabilen, kanonischen Namen, damit die Daten nicht über Formatierungsvarianten hinweg fragmentiert werden.
