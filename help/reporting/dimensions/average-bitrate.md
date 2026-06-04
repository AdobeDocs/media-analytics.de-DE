---
title: Durchschnittliche Bitrate (Dimension)
description: Gibt die gepackte durchschnittliche Bitrate jeder Sitzung in Intervallen von 100 kBit/s an.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Durchschnittliche Bitrate (Dimension)

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Dimension **Durchschnittliche Bitrate**behandelt, die die Bucket-Bitrate jeder Sitzung angibt. Siehe [Durchschnittliche Bitrate (Metrik)](/help/reporting/metrics/average-bitrate.md) für die Metrik „Roher gewichteter Durchschnitt“. Siehe [Bitrate](/help/implementation/variables/quality/bitrate.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Durchschnittliche Bitrate** zeigt die durchschnittliche Wiedergabebitrate pro Sitzung an, die in Intervallen von 100 kBit/s zusammengefasst ist. Das Backend berechnet den Wert als gewichteten Durchschnitt aller Bitratenwerte über die Sitzung und weist ihn dann einem Bucket zu. Verwenden Sie die Dimension, um die Interaktion und Qualität nach Bitratenebene aufzuschlüsseln.

## So wird diese Dimension ausgefüllt

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.bitrateAverageBucket`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## Dimensionselemente

Jedes Element ist eine Beschriftung für einen Bitraten-Bucket (z. B. `800-899`, `3200-3299`). Verwenden Sie die [Durchschnittliche Bitrate (Metrik)](/help/reporting/metrics/average-bitrate.md) für einen rohen gewichteten Durchschnittswert anstelle einer Dimension mit Buckets.
