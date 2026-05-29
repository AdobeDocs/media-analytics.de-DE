---
title: Beschriftung
description: Meldet das Plattenlabel, unter dem der Audioinhalt freigegeben wurde.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 10%

---


# Beschriftung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Beschriftung**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/standard-metadata/label.md) unter „Bezeichnung“*

>[!ENDSHADEBOX]

Die **label**-Dimension zeigt die Plattenfirma an, die den Audioinhalt freigegeben hat (z. B. `"Capitol Records"`). Verwenden Sie diese Option, um die Interaktion zwischen Labels in einem Musik- oder Podcast-Katalog zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Beschriftung wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.label`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## Dimensionselemente

Jedes Element ist der literale Bezeichnungsname, der beim Sitzungsstart gemeldet wird. Verwenden Sie für jedes Label einen stabilen, kanonischen Namen, damit die Interaktion nicht über Rechtschreib- oder Aufdruckvarianten hinweg fragmentiert.
