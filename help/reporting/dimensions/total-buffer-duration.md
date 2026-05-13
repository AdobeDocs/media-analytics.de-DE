---
title: Gesamtdauer des Puffers (Dimension)
description: Gibt die kumulierten Pufferzeiten pro Sitzung an.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 5%

---


# Gesamtdauer des Puffers (Dimension)

>[!BEGINSHADEBOX]

*Diese Seite deckt die Dimension **Gesamtdauer des Puffers**&#x200B;ab. Adobe Analytics füllt automatisch eine gepaarte [Gesamtpufferdauer (Metrik)](/help/reporting/metrics/total-buffer-duration.md) aus derselben `a.media.qoe.bufferTime` Kontextdatenvariablen. Customer Journey Analytics stellt ein einzelnes `mediaReporting.qoeDataDetails.bufferTime` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Dimension **Gesamtpufferdauer** zeigt die kumulative Zeit in Sekunden an, die der Player während einer Sitzung in einem Pufferstatus verbracht hat. Verwenden Sie die Dimension, um die Interaktion nach dem genauen Wert der Pufferdauer aufzuheben.

## So wird diese Dimension ausgefüllt

Das Medien-Backend addiert die Dauer jedes Pufferintervalls (von `media.bufferStart` bis zur nächsten Statusänderung). Der Wert wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bufferTime`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebuffertimeevar, post_videoqoebuffertimeevar` |

## Dimensionselemente

Jedes Element ist der literale Dauerwert in Sekunden, der beim Schließen-Aufruf gemeldet wird.
