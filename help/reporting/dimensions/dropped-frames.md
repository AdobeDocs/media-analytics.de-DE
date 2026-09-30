---
title: Abgelegte Frames (Dimension)
description: Gibt die kumulative Anzahl der Dropped Frames pro Sitzung an.
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
source-wordcount: '183'
ht-degree: 7%
---

# Abgelegte Frames (Dimension)

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Dimension **Abgelegte Frames**. Adobe Analytics füllt automatisch eine paarweise [Abgelegte Frames (Metrik](/help/reporting/metrics/dropped-frames.md) aus derselben `a.media.qoe.droppedFrameCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.droppedFrames` bereit, das Sie als Dimension oder Metrik verwenden können. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/quality/dropped-frames.md) unter „Abgelegte Frames“*

>[!ENDSHADEBOX]

Die Dimension **Abgelegte Frames** zeigt die kumulative Anzahl der Frames an, die während einer Sitzung abgelegt wurden. Verwenden Sie die Dimension, um die Interaktion durch eine exakte Ablageanzahl aufzuheben.

## So wird diese Dimension ausgefüllt

Der Player aktualisiert den `droppedFrames` des QoE-Objekts, während es Abfälle sammelt. Das Backend meldet den neuesten Wert beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.droppedFrameCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## Dimensionselemente

Jedes Element ist der beim Schließen-Aufruf gemeldete literale Dropcount-Wert. Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob Frames überhaupt abgelegt wurden) [von abgelegten Frames betroffene Streams](/help/reporting/metrics/dropped-frame-impacted-streams.md).
