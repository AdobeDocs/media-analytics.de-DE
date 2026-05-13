---
title: Teil des Tages
description: Gibt die Tageszeit (Morgen, Nachmittag, Primetime, Late Night) an, zu der der Inhalt gesendet oder wiedergegeben wurde.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 6%

---


# Teil des Tages

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Day-Teil**behandelt. Siehe [Day-Teil](/help/implementation/variables/standard-metadata/day-part.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Tagesteil** zeigt den Tageszeit-Bucket an, in dem der Inhalt gesendet oder wiedergegeben wurde. Häufige Werte sind `"Morning"`, `"Afternoon"`, `"Primetime"` und `"Late Night"`. Damit können Sie die Interaktion über Tagesbereiche hinweg unabhängig von der lokalen Zeitzone des Betrachters vergleichen.

## So wird diese Dimension ausgefüllt

Der Tagesabschnitt wird vom Player beim Sitzungsbeginn festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.dayPart`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videodaypart, post_videodaypart` |

## Dimensionselemente

Jedes Element ist die eigentliche DayPart-Beschriftung, die beim Sitzungsstart gemeldet wird. Verwenden Sie einen festen Satz von Werten über Implementierungen hinweg, um Zeilenelemente konsistent zu halten.
