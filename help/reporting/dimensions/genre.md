---
title: Genre
description: Berichte zum Inhaltsgenre. Inhalte mit mehreren Genres werden auf mehrere Zeileneinträge aufgeteilt, wobei jede das gleiche Metrikgewicht erhält.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---


# Genre

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Genre**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/genre.md) unter „Genre“*

>[!ENDSHADEBOX]

Die Dimension **Genre** zeigt das Inhaltsgenre an. Das Genre wird als kommagetrennte Zeichenfolge erfasst und als Listendimension gespeichert. Inhalte mit mehreren Genres werden auf separate Zeileneinträge aufgeteilt, wobei jede das gleiche Metrikgewicht erhält. Damit können Sie die Interaktion zwischen den Genres vergleichen, ohne die Zeit, die mit einem einzelnen Asset mit mehreren Genres verbracht wird, doppelt zu zählen.

## So wird diese Dimension ausgefüllt

Das Genre wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem `a.media.genre` „Kontextdaten“ erfasst (als Listenvariable gespeichert), wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) oder [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) (alt) |
| Daten-Feeds | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Dimensionselemente

Jedes Element ist ein Genre-Wert. Multi-Genre-Sitzungen (z. B. `"Drama,Action"`) werden als zwei separate Zeileneinträge (`Drama` und `Action`) angezeigt, wobei jedem Element die volle Gewichtung für die Sitzung zugewiesen wird.
