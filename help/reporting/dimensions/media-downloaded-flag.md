---
title: Medien heruntergeladen
description: Kennzeichnet Sitzungen, in denen heruntergeladene Offline-Inhalte wiedergegeben werden.
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
source-wordcount: '195'
ht-degree: 7%
---

# Medien heruntergeladen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Medien heruntergeladen**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/core/media-downloaded-flag.md) unter „Media Downloaded Flag*

>[!ENDSHADEBOX]

Die Dimension **Medien heruntergeladen** kennzeichnet Sitzungen, in denen zuvor heruntergeladene Offline-Inhalte und kein Live-Stream aus dem Internet wiedergegeben wurden. Verwenden Sie diese Option, um die Offline-Wiedergabe von gestreamten Sitzungen zu trennen, wenn Interaktion, Abschluss oder Qualität verglichen werden.

## So wird diese Dimension ausgefüllt

Das Flag für den Download wird vom Player auf eine von drei Arten festgelegt. Initialisieren Sie den Tracker mit dem Flag (Mobile SDK), senden Sie den `sessionStart` an die `/downloaded`-Endpunktvariante (Media Edge API Direct) oder schließen Sie `media.downloaded: true` in die `sessionStart` ein (Mediensammlungs-API).

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.downloaded` einer eVar zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.downloaded` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## Dimensionselemente

| Wert | Beschreibung |
| --- | --- |
| `true` | Die Sitzung hat heruntergeladene Offline-Inhalte wiedergegeben. |
| (leer) | Die Sitzung spielte einen Live-Stream ab. Das Feld wird ausgelassen, anstatt auf `false` gesetzt zu werden. |
