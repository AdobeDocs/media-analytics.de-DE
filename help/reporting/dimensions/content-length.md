---
title: Länge des Inhalts
description: Gibt die Gesamtdauer jeder Mediensitzung in Sekunden an, wie bei Sitzungsbeginn festgelegt.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%

---


# Länge des Inhalts

>[!BEGINSHADEBOX]

*Diese Seite deckt die Berichtsdimension **Inhaltslänge**&#x200B;ab. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/content-length.md) unter „Inhaltslänge“*

>[!ENDSHADEBOX]

Die Dimension **Inhaltslänge** zeigt die Gesamtdauer in Sekunden jeder Mediensitzung an, wie sie beim Sitzungsstart festgelegt wurde. Es unterstützt Backend-Metriken, einschließlich [Fortschrittsmarken](/help/reporting/metrics/progress-markers.md) und [Zielgruppendurchschnitt pro Minute](/help/reporting/metrics/average-minute-audience.md).

## So wird diese Dimension ausgefüllt

Die Inhaltslänge wird vom Player beim Sitzungsstart festgelegt. Der gemeldete Wert ist die vollständige Dauer des Assets in Sekunden, nicht der verstrichene Abspielkopf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.length`, wenn [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>In Adobe Analytics entspricht dieser Wert auch einer Klassifizierung **Videolänge** in der Dimension [Inhalt](content.md). Sie sind dafür verantwortlich, diese Klassifizierung separat auszufüllen und zu pflegen. Customer Journey Analytics verwendet diese Dimension direkt. Sie können bei [&#x200B; Wert-](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing) verwenden.

>[!IMPORTANT]
>
>Wenn die Inhaltslänge nicht festgelegt ist oder nicht größer als null ist, werden für diese Sitzung keine Fortschrittsmarken und kein Zielgruppendurchschnitt pro Minute erstellt. Für Live-Streams mit unbekannter Dauer `86400` festlegen.

## Dimensionselemente

Jedes Element ist der literale Längenwert in Sekunden, der beim Sitzungsstart gemeldet wird.
