---
title: Beschriftung
description: Meldet das Plattenlabel, unter dem der Audioinhalt freigegeben wurde.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# Beschriftung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Beschriftung**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/label.md) unter „Bezeichnung“*

>[!ENDSHADEBOX]

Die **label**-Dimension zeigt die Plattenfirma an, die den Audioinhalt freigegeben hat (z. B. `"Capitol Records"`). Verwenden Sie diese Option, um die Interaktion zwischen Labels in einem Musik- oder Podcast-Katalog zu vergleichen.

## So wird diese Dimension ausgefüllt

Die Beschriftung wird vom Player beim Sitzungsstart für Audioinhalte festgelegt.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.label`, wenn [[!UICONTROL Audio-]](/help/reporting/media-reports-enable.md)) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoaudiolabel` |

## Dimensionselemente

Jedes Element ist der literale Bezeichnungsname, der beim Sitzungsstart gemeldet wird. Verwenden Sie für jedes Label einen stabilen, kanonischen Namen, damit die Interaktion nicht über Rechtschreib- oder Aufdruckvarianten hinweg fragmentiert.
