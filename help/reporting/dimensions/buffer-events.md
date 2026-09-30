---
title: Pufferereignisse (Dimension)
description: Gibt die Anzahl der Pufferereignisse pro Sitzung an.
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
source-wordcount: '175'
ht-degree: 8%
---

# Pufferereignisse (Dimension)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Dimension **Pufferereignisse**behandelt. Adobe Analytics füllt automatisch eine gepaarte [Pufferereignis (Metrik)](/help/reporting/metrics/buffer-events.md) aus derselben `a.media.qoe.bufferCount` Kontextdatenvariablen. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.bufferCount` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Dimension **Pufferereignisse** zeigt die Anzahl der Pufferereignisse an, die während einer Sitzung aufgetreten sind. Verwenden Sie die Dimension, um die Interaktion anhand der genauen Pufferanzahl aufzuheben.

## So wird diese Dimension ausgefüllt

Das Medien-Backend erhöht die Anzahl jedes Mal, wenn der Player in einen `buffer` eintritt. Der Wert wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bufferCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Dimensionselemente

Jedes Element ist der beim Schließen-Aufruf gemeldete literale Wert der Pufferanzahl. Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob in der Sitzung überhaupt Puffer aufgetreten sind[ „Vom Puffer betroffene Streams](/help/reporting/metrics/buffer-impacted-streams.md).
