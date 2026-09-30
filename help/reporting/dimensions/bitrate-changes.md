---
title: Änderungen der Bitrate (Dimension)
description: Gibt die Anzahl der Bitratenänderungsereignisse pro Sitzung an.
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
source-wordcount: '205'
ht-degree: 6%
---

# Änderungen der Bitrate (Dimension)

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Dimension **Bitratenänderungen**. Adobe Analytics füllt automatisch eine gepaarte [Bitratenänderungen (Metrik)](/help/reporting/metrics/bitrate-changes.md) aus derselben `a.media.qoe.bitrateChangeCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` bereit, das Sie als Dimension oder Metrik verwenden können. Siehe [Bitratenänderung](/help/implementation/variables/quality/bitrate-change.md), wie Sie Bitratenänderungsereignisse auslösen.*

>[!ENDSHADEBOX]

Die Dimension **Bitratenänderungen** zeigt die Anzahl der Bitratenänderungsereignisse an, die während einer Sitzung aufgetreten sind. Verwenden Sie die Dimension , um Interaktion und Qualität anhand des genauen Werts der Änderungsanzahl auszubrechen (z. B. „Sitzungen mit 3 Bitratenänderungen vs. Sitzungen mit 0„).

## So wird diese Dimension ausgefüllt

Das Medien-Backend erhöht die Anzahl bei jedem [Bitratenänderung](/help/implementation/events/playback/bitrate-change.md), das während der Sitzung empfangen wurde. Der Wert wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateChangeCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## Dimensionselemente

Jedes Element ist der literale Änderungszählungswert, der beim Schließen-Aufruf gemeldet wird. Verwenden Sie für das Reporting über boolesche Werte auf Sitzungsebene (unabhängig davon, ob in der Sitzung überhaupt eine Bitratenänderung aufgetreten ist) [ Streams, die von Bitratenänderungen betroffen ](/help/reporting/metrics/bitrate-change-impacted-streams.md).
