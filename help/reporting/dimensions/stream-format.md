---
title: Stream-Format
description: Gibt die Qualitätsstufe jeder Sitzung an (normalerweise HD oder SD).
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
source-wordcount: '168'
ht-degree: 7%
---

# Stream-Format

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Stream-Format**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/stream-format.md) unter „Stream-Format*

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
