---
title: Bitratenänderungen (Metrik)
description: Zählt Ereignisse mit Bitratenänderungen für Summen und Durchschnittswerte über Sitzungen hinweg.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 7%
---

# Bitratenänderungen (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Bitratenänderungen**&#x200B;behandelt. Adobe Analytics füllt automatisch eine gepaarte [Bitratenänderungen (Dimension](/help/reporting/dimensions/bitrate-changes.md) aus derselben `a.media.qoe.bitrateChangeCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` bereit, das Sie als Dimension oder Metrik verwenden können. Siehe [Bitratenänderung](/help/implementation/variables/quality/bitrate-change.md), wie Sie Bitratenänderungsereignisse auslösen.*

>[!ENDSHADEBOX]

Die Metrik **Bitratenänderungen** zählt Ereignisse von Bitratenänderungen über Sitzungen hinweg und ist für Summen, Durchschnittswerte und Perzentil-Rollups geeignet. Verwenden Sie die -Metrik, um das Gesamtvolumen der Bitratenänderungen in einem Berichtszeitraum zu berechnen und die Bitratenstabilität zwischen Inhalten, Netzwerken oder Playern zu vergleichen.

## Berechnung dieser Metrik

Das Medien-Backend erhöht die Anzahl bei jedem [Bitratenänderung](/help/implementation/events/playback/bitrate-change.md), das während der Sitzung empfangen wurde. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateChangeCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

Verwenden Sie für das Reporting über boolesche Werte auf Sitzungsebene (unabhängig davon, ob in der Sitzung überhaupt eine Bitratenänderung aufgetreten ist) [&#x200B; Streams, die von Bitratenänderungen betroffen &#x200B;](bitrate-change-impacted-streams.md).
