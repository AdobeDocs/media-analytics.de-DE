---
title: Durchschnittliche Bitrate (Dimension)
description: Gibt die gepackte durchschnittliche Bitrate jeder Sitzung in Intervallen von 100 kBit/s an.
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
source-wordcount: '170'
ht-degree: 8%
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
