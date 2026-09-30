---
title: Datum der Erstausstrahlung
description: Meldet das Datum, an dem der Inhalt erstmals im Fernsehen ausgestrahlt wurde.
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
source-wordcount: '403'
ht-degree: 1%
---

# Datum der Erstausstrahlung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Erstes Sendedatum**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/first-air-date.md) unter „Erstes Sendedatum“*

>[!ENDSHADEBOX]

Die Dimension **Datum der ersten Ausstrahlung** gibt das Datum an, an dem der Inhalt erstmals im Fernsehen ausgestrahlt wurde. Verwenden Sie diese Option, um die Interaktion bei neuen Versionen von der Interaktion mit älteren Inhalten zu trennen.

## So wird diese Dimension ausgefüllt

Das Datum der ersten Ausstrahlung wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.airDate` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Inhalt (ID](content.md) . Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.airDate` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.airDate` |

## Klassifizierungsansatz

Adobe erstellt die Klassifizierungsstruktur für das erste Sendedatum automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1:1-Beziehung zwischen jeder Inhalts-ID und ihrem ersten Sendedatum. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Namen der Klassifizierung für das erste Flugdatum. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.airDate` einer eVar zuordnet. Dieser Ansatz erfasst das erste Sendedatum als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1:1-Beziehung zwischen dem ersten Sendedatum und der übergeordneten Dimension [Inhalt (ID)](content.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Inhalts-ID über Ereignisse hinweg sendet, können mehrere erste Sendedaten unter demselben Inhalt angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist die beim Sitzungsbeginn gemeldete Datums-Literalzeichenfolge. Verwenden Sie ein konsistentes Format für alle Implementierungen. Adobe empfiehlt `YYYY-MM-DD`.
