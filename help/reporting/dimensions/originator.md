---
title: Urheber
description: Gibt den Ersteller oder das Produktionsstudio des Inhalts an.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---


# Urheber

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Urheber**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/originator.md) unter „Urheber“*

>[!ENDSHADEBOX]

Die Dimension **Urheber** meldet den Ersteller oder das Produktionsstudio des Inhalts (z. B. `"Warner Brothers"` oder `"Sony"`). Verwenden Sie sie, um die Interaktion zwischen Inhaltsinhabern oder Rechteinhabern zu vergleichen.

## So wird diese Dimension ausgefüllt

Der Urheber wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.originator` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Inhalt (ID)](content.md) - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.originator` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.originator` |

## Klassifizierungsansatz

Adobe erstellt die ursprüngliche Klassifizierungsstruktur automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[ auszufüllen und zu ](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Inhalts-ID und ihrem Urheber. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Namen der ursprünglichen Klassifizierung. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.originator` einer eVar zuordnet. Dieser Ansatz erfasst den Urheber als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen dem Urheber und der übergeordneten Dimension [Content (ID)](content.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Inhalts-ID über Ereignisse hinweg sendet, können mehrere Urheber unter demselben Inhalt erscheinen. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist der bei Sitzungsbeginn gemeldete literale Ursprungswert. Verwenden Sie einen stabilen, eindeutigen Namen pro Studio, damit die Interaktion nicht über nicht verwandte Entitäten hinweg reduziert wird.
