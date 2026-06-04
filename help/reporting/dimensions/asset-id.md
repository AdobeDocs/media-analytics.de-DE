---
title: Element-ID
description: Gibt eine stabile Branchenkennung für das zugrunde liegende Medien-Asset an.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# Element-ID

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Asset-ID**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/asset-id.md) unter „Asset-ID“*

>[!ENDSHADEBOX]

Die Dimension **Asset-ID** zeigt eine stabile Branchenkennung für das zugrunde liegende Medien-Asset an (normalerweise eine EIDR-, TMS/Gracenote- oder Rovi-ID, aber proprietäre IDs werden ebenfalls akzeptiert).

## So wird diese Dimension ausgefüllt

Die Asset-ID wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics (Verarbeitungsregel) | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.asset` einer eVar zuordnet. |
| Adobe Analytics (Klassifizierung) | Klassifizierung der Dimension [Inhalt (ID)](content.md) - Adobe erstellt diese Klassifizierung automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind für das Ausfüllen und Verwalten von Classification-Werten verantwortlich. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds (Verarbeitungsregel) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.asset` zugeordnet ist) |
| Daten-Feeds (Klassifizierung) | K. A. - Daten-Feeds unterstützen keine Klassifizierungen. |
| Audience Manager | `c_contextdata.a.media.asset` |

## Klassifizierungsansatz

Adobe erstellt die Asset-ID-Klassifizierungsstruktur automatisch, wenn **[[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md)** für die Report Suite aktiviert ist. Sie sind dafür verantwortlich, die Klassifizierung mithilfe von „Klassifizierungssätze[&#x200B; auszufüllen und zu &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Dieser Ansatz bietet eine garantierte 1::1-Beziehung zwischen jeder Inhalts-ID und ihrer Asset-ID. Klassifizierungsaktualisierungen gelten rückwirkend für alle historischen Daten für diese ID.

>[!IMPORTANT]
>
>Ändern Sie nicht den Asset-ID-Klassifizierungsnamen. Das Umbenennen kann dazu führen, dass Adobe die ursprüngliche Klassifizierung neu erstellt, was zu einem Duplikat führt.

## Ansatz der Verarbeitungsregeln

Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.asset` einer eVar zuordnet. Dieser Ansatz erfasst die Asset-ID als Wert pro Treffer, ohne dass eine Klassifizierungswartung erforderlich ist.

Der Nachteil besteht darin, dass Sie die garantierte 1::1-Beziehung zwischen der Asset-ID und der übergeordneten Dimension [Content (ID)](content.md) verlieren. Wenn Ihre Implementierung inkonsistente Werte für dieselbe Inhalts-ID über Ereignisse hinweg sendet, können mehrere Asset-IDs unter demselben Inhalt angezeigt werden. Die Aktualisierung eines Werts gilt nur für Daten, die in Zukunft verwendet werden.

## Dimensionselemente

Jedes Element ist ein eindeutiger Asset-ID-Wert, der im Berichtszeitraum gemeldet wurde. Verwenden Sie eine einzige stabile Kennung pro Asset für alle Verteilungsplattformen, sodass derselbe Inhalt zu einem einzigen Zeileneintrag aggregiert wird.
