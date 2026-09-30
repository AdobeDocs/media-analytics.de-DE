---
title: Teil des Tages
description: Gibt die Tageszeit (Morgen, Nachmittag, Primetime, Late Night) an, zu der der Inhalt gesendet oder wiedergegeben wurde.
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
source-wordcount: '151'
ht-degree: 9%
---

# Teil des Tages

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Day-Teil**&#x200B;behandelt. Siehe [Day-Teil](/help/implementation/variables/standard-metadata/day-part.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Tagesteil** zeigt den Tageszeit-Bucket an, in dem der Inhalt gesendet oder wiedergegeben wurde. Häufige Werte sind `"Morning"`, `"Afternoon"`, `"Primetime"` und `"Late Night"`. Damit können Sie die Interaktion über Tagesbereiche hinweg unabhängig von der lokalen Zeitzone des Betrachters vergleichen.

## So wird diese Dimension ausgefüllt

Der Tagesabschnitt wird vom Player beim Sitzungsbeginn festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.dayPart`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## Dimensionselemente

Jedes Element ist die eigentliche DayPart-Beschriftung, die beim Sitzungsstart gemeldet wird. Verwenden Sie einen festen Satz von Werten über Implementierungen hinweg, um Zeilenelemente konsistent zu halten.
