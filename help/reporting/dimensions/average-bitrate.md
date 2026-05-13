---
title: Durchschnittliche Bitrate (Dimension)
description: Gibt die gepackte durchschnittliche Bitrate jeder Sitzung in Intervallen von 100 kBit/s an.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# Durchschnittliche Bitrate (Dimension)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Dimension **Durchschnittliche Bitrate**&#x200B;behandelt, die die Bucket-Bitrate jeder Sitzung angibt. Siehe [Durchschnittliche Bitrate (Metrik)](/help/reporting/metrics/average-bitrate.md) für die Metrik „Roher gewichteter Durchschnitt“. Siehe [Bitrate](/help/implementation/variables/quality/bitrate.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Durchschnittliche Bitrate** zeigt die durchschnittliche Wiedergabebitrate pro Sitzung an, die in Intervallen von 100 kBit/s zusammengefasst ist. Das Backend berechnet den Wert als gewichteten Durchschnitt aller Bitratenwerte über die Sitzung und weist ihn dann einem Bucket zu. Verwenden Sie die Dimension, um die Interaktion und Qualität nach Bitratenebene aufzuschlüsseln.

## So wird diese Dimension ausgefüllt

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateAverageBucket`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebitrateaverageevar, post_videoqoebitrateaverageevar` |

## Dimensionselemente

Jedes Element ist eine Beschriftung für einen Bitraten-Bucket (z. B. `800-899`, `3200-3299`). Verwenden Sie die [Durchschnittliche Bitrate (Metrik)](/help/reporting/metrics/average-bitrate.md) für einen rohen gewichteten Durchschnittswert anstelle einer Dimension mit Buckets.
