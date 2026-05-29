---
title: Stream-Format
description: Gibt die Qualitätsstufe jeder Sitzung an (normalerweise HD oder SD).
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Stream-Format

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Stream-Format**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/stream-format.md) unter „Stream-Format*

>[!ENDSHADEBOX]

Die Dimension **Stream-**) zeigt die Qualitätsstufe jeder Sitzung an (normalerweise `"HD"` oder `"SD"`, aber jede Zeichenfolge wird akzeptiert). Verwenden Sie sie, um Interaktion, Abschluss und Qualität über die verschiedenen Bereitstellungs-Qualitätsstufen hinweg zu vergleichen.

## So wird diese Dimension ausgefüllt

Das Stream-Format wird vom Player beim Sitzungsstart festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.format` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.format` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.format` |

## Dimensionselemente

Jedes Element ist der beim Sitzungsbeginn gemeldete Literalformatwert. Verwenden Sie einen stabilen Satz von Werten (`HD`, `SD`, `4K`, `UHD`), damit Zeileneinträge nicht über Schreibvarianten hinweg fragmentiert werden.
