---
title: Änderungen der Bitrate (Dimension)
description: Gibt die Anzahl der Bitratenänderungsereignisse pro Sitzung an.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 5%

---


# Änderungen der Bitrate (Dimension)

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Dimension **Bitratenänderungen**. Adobe Analytics füllt automatisch eine gepaarte [Bitratenänderungen (Metrik)](/help/reporting/metrics/bitrate-changes.md) aus derselben `a.media.qoe.bitrateChangeCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `mediaReporting.qoeDataDetails.bitrateChangeCount` bereit, das Sie als Dimension oder Metrik verwenden können. Siehe [Bitratenänderung](/help/implementation/variables/quality/bitrate-change.md), wie Sie Bitratenänderungsereignisse auslösen.*

>[!ENDSHADEBOX]

Die Dimension **Bitratenänderungen** zeigt die Anzahl der Bitratenänderungsereignisse an, die während einer Sitzung aufgetreten sind. Verwenden Sie die Dimension , um Interaktion und Qualität anhand des genauen Werts der Änderungsanzahl auszubrechen (z. B. „Sitzungen mit 3 Bitratenänderungen vs. Sitzungen mit 0„).

## So wird diese Dimension ausgefüllt

Das Medien-Backend erhöht die Anzahl bei jedem während der Sitzung empfangenen `media.bitrateChange`. Der Wert wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateChangeCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebitratechangecountevar, post_videoqoebitratechangecountevar` |

## Dimensionselemente

Jedes Element ist der literale Änderungszählungswert, der beim Schließen-Aufruf gemeldet wird. Verwenden Sie für das Reporting über boolesche Werte auf Sitzungsebene (unabhängig davon, ob in der Sitzung überhaupt eine Bitratenänderung aufgetreten ist) [ Streams, die von Bitratenänderungen betroffen ](/help/reporting/metrics/bitrate-change-impacted-streams.md).
