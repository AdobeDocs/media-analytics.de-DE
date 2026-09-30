---
title: Durchschnittliche Bitrate (Metrik)
description: Gibt die rohe gewichtete durchschnittliche Bitrate jeder Sitzung in kBit/s an.
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
source-wordcount: '175'
ht-degree: 8%
---

# Durchschnittliche Bitrate (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Ereignismetrik **Durchschnittliche Bitrate**&#x200B;behandelt, die die rohe gewichtete durchschnittliche Bitrate pro Sitzung ausgibt. Siehe [Durchschnittliche Bitrate (Dimension)](/help/reporting/dimensions/average-bitrate.md) für die Dimension mit Buckets. Siehe [Bitrate](/help/implementation/variables/quality/bitrate.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Metrik **Durchschnittliche Bitrate** zeigt die rohe gewichtete durchschnittliche Wiedergabebitrate in kbps für jede Sitzung an. Im Gegensatz zur [Dimension mit Buckets](/help/reporting/dimensions/average-bitrate.md) ist die Metrik ein fortlaufender numerischer Wert, der für Summen, Durchschnittswerte und Perzentil-Rollups über Sitzungen hinweg geeignet ist.

## Berechnung dieser Metrik

Das Medien-Backend berechnet einen gewichteten Durchschnitt aller während der Sitzung gemeldeten Bitratenwerte, gewichtet durch die Dauer, während der jede Bitrate aktiv war. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateAverage`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverage` |
