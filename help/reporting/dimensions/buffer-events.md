---
title: Pufferereignisse (Dimension)
description: Gibt die Anzahl der Pufferereignisse pro Sitzung an.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---


# Pufferereignisse (Dimension)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Dimension **Pufferereignisse**&#x200B;behandelt. Adobe Analytics füllt automatisch eine gepaarte [Pufferereignis (Metrik)](/help/reporting/metrics/buffer-events.md) aus derselben `a.media.qoe.bufferCount` Kontextdatenvariablen. Customer Journey Analytics stellt ein einzelnes `mediaReporting.qoeDataDetails.bufferCount` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Dimension **Pufferereignisse** zeigt die Anzahl der Pufferereignisse an, die während einer Sitzung aufgetreten sind. Verwenden Sie die Dimension, um die Interaktion anhand der genauen Pufferanzahl aufzuheben.

## So wird diese Dimension ausgefüllt

Das Medien-Backend erhöht die Anzahl jedes Mal, wenn der Player in einen `buffer` eintritt. Der Wert wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bufferCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Dimensionselemente

Jedes Element ist der beim Schließen-Aufruf gemeldete literale Wert der Pufferanzahl. Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob in der Sitzung überhaupt Puffer aufgetreten sind[&#x200B; „Vom Puffer betroffene Streams](/help/reporting/metrics/buffer-impacted-streams.md).
