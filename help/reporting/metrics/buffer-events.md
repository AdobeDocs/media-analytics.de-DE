---
title: Pufferereignisse (Metrik)
description: Zählt Pufferereignisse für Summen und Durchschnittswerte über Sitzungen hinweg.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# Pufferereignisse (Metrik)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Metrik **Pufferereignisse**&#x200B;behandelt. Adobe Analytics füllt automatisch eine gepaarte [Pufferereignis (Dimension](/help/reporting/dimensions/buffer-events.md) aus derselben `a.media.qoe.bufferCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.bufferCount` bereit, das Sie als Dimension oder Metrik verwenden können.*

>[!ENDSHADEBOX]

Die Metrik **Pufferereignisse** zählt Pufferereignisse über Sitzungen hinweg und eignet sich für Summen, Durchschnittswerte und Perzentil-Rollups. Verwenden Sie die -Metrik, um das Gesamtpuffervolumen über einen Berichtszeitraum zu berechnen und die Pufferstabilität über Inhalte, Netzwerke oder Player hinweg zu vergleichen.

## Berechnung dieser Metrik

Das Medien-Backend erhöht die Anzahl jedes Mal, wenn der Player in einen [Pufferstart](/help/implementation/events/playback/buffer-start.md)-Status wechselt. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bufferCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob in der Sitzung überhaupt Puffer aufgetreten sind[&#x200B; „Vom Puffer betroffene Streams](buffer-impacted-streams.md).
