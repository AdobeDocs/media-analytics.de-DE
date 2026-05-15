---
title: Medien heruntergeladen
description: Kennzeichnet Sitzungen, in denen heruntergeladene Offline-Inhalte wiedergegeben werden.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# Medien heruntergeladen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Medien heruntergeladen**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/core/media-downloaded-flag.md) unter „Media Downloaded Flag*

>[!ENDSHADEBOX]

Die Dimension **Medien heruntergeladen** kennzeichnet Sitzungen, in denen zuvor heruntergeladene Offline-Inhalte und kein Live-Stream aus dem Internet wiedergegeben wurden. Verwenden Sie diese Option, um die Offline-Wiedergabe von gestreamten Sitzungen zu trennen, wenn Interaktion, Abschluss oder Qualität verglichen werden.

## So wird diese Dimension ausgefüllt

Das Flag für den Download wird vom Player auf eine von drei Arten festgelegt. Initialisieren Sie den Tracker mit dem Flag (Mobile SDK), senden Sie den `sessionStart` an die `/downloaded`-Endpunktvariante (Media Edge API Direct) oder schließen Sie `media.downloaded: true` in die `sessionStart` ein (Mediensammlungs-API).

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.downloaded` einer eVar zuordnet. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `evar1`-`evar250`, `post_evar1`-`post_evar250` (die eVar, der Ihre Verarbeitungsregel `a.media.downloaded` zugeordnet ist) |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## Dimensionselemente

| Wert | Beschreibung |
| --- | --- |
| `true` | Die Sitzung hat heruntergeladene Offline-Inhalte wiedergegeben. |
| (leer) | Die Sitzung spielte einen Live-Stream ab. Das Feld wird ausgelassen, anstatt auf `false` gesetzt zu werden. |
