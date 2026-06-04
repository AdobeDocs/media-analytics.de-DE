---
title: Abgelegte Frames (Dimension)
description: Gibt die kumulative Anzahl der Dropped Frames pro Sitzung an.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---


# Abgelegte Frames (Dimension)

>[!BEGINSHADEBOX]

*Diese Seite behandelt die Dimension **Abgelegte Frames**. Adobe Analytics füllt automatisch eine paarweise [Abgelegte Frames (Metrik](/help/reporting/metrics/dropped-frames.md) aus derselben `a.media.qoe.droppedFrameCount` Kontextdatenvariablen aus. Customer Journey Analytics stellt ein einzelnes `xdm.mediaReporting.qoeDataDetails.droppedFrames` bereit, das Sie als Dimension oder Metrik verwenden können. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/quality/dropped-frames.md) unter „Abgelegte Frames“*

>[!ENDSHADEBOX]

Die Dimension **Abgelegte Frames** zeigt die kumulative Anzahl der Frames an, die während einer Sitzung abgelegt wurden. Verwenden Sie die Dimension, um die Interaktion durch eine exakte Ablageanzahl aufzuheben.

## So wird diese Dimension ausgefüllt

Der Player aktualisiert den `droppedFrames` des QoE-Objekts, während es Abfälle sammelt. Das Backend meldet den neuesten Wert beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.droppedFrameCount`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## Dimensionselemente

Jedes Element ist der beim Schließen-Aufruf gemeldete literale Dropcount-Wert. Verwenden Sie für das boolesche Reporting auf Sitzungsebene (unabhängig davon, ob Frames überhaupt abgelegt wurden) [von abgelegten Frames betroffene Streams](/help/reporting/metrics/dropped-frame-impacted-streams.md).
