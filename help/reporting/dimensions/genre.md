---
title: Genre
description: Berichte zum Inhaltsgenre. Inhalte mit mehreren Genres werden auf mehrere Zeileneinträge aufgeteilt, wobei jede das gleiche Metrikgewicht erhält.
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
source-wordcount: '181'
ht-degree: 8%
---

# Genre

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Genre**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/genre.md) unter „Genre“*

>[!ENDSHADEBOX]

Die Dimension **Genre** zeigt das Inhaltsgenre an. Das Genre wird als kommagetrennte Zeichenfolge erfasst und als Listendimension gespeichert. Inhalte mit mehreren Genres werden auf separate Zeileneinträge aufgeteilt, wobei jede das gleiche Metrikgewicht erhält. Damit können Sie die Interaktion zwischen den Genres vergleichen, ohne die Zeit, die mit einem einzelnen Asset mit mehreren Genres verbracht wird, doppelt zu zählen.

## So wird diese Dimension ausgefüllt

Das Genre wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem `a.media.genre` „Kontextdaten“ erfasst (als Listenvariable gespeichert), wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) oder [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) (alt) |
| Daten-Feeds | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Dimensionselemente

Jedes Element ist ein Genre-Wert. Multi-Genre-Sitzungen (z. B. `"Drama,Action"`) werden als zwei separate Zeileneinträge (`Drama` und `Action`) angezeigt, wobei jedem Element die volle Gewichtung für die Sitzung zugewiesen wird.
