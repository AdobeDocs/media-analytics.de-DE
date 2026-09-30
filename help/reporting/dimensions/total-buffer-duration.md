---
title: Gesamtdauer des Puffers (Dimension)
description: Gibt die kumulierten Pufferzeiten pro Sitzung an.
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
source-wordcount: '194'
ht-degree: 7%
---

# Gesamtdauer des Puffers (Dimension)

>[!BEGINSHADEBOX]

*Diese Seite deckt die Dimension **Gesamtdauer des Puffers**&#x200B;ab. Adobe Analytics füllt automatisch eine gepaarte [Gesamtpufferdauer (Metrik)](/help/reporting/metrics/total-buffer-duration.md) aus derselben `a.media.qoe.bufferTime` Kontextdatenvariablen. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.bufferTime` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Dimension **Gesamtpufferdauer** zeigt die kumulative Zeit in Sekunden an, die der Player während einer Sitzung in einem Pufferstatus verbracht hat. Verwenden Sie die Dimension, um die Interaktion nach dem genauen Wert der Pufferdauer aufzuheben.

## So wird diese Dimension ausgefüllt

Das Medien-Backend addiert die Dauer jedes Pufferintervalls (von [Pufferstart](/help/implementation/events/playback/buffer-start.md) bis zur nächsten Statusänderung). Der Wert wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bufferTime`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## Dimensionselemente

Jedes Element ist der literale Dauerwert in Sekunden, der beim Schließen-Aufruf gemeldet wird.
