---
title: Player SDK-Fehler-IDs
description: meldet eindeutige Fehler-IDs, die vom Content Player SDK generiert wurden.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 6%

---


# Player SDK-Fehler-IDs

Die Dimension **Player-SDK-Fehler** IDs“ zeigt eindeutige Fehlerkennungen an, die vom Content-Player-SDK während einer Sitzung generiert wurden. Der Player muss die Codes oder IDs zur Implementierungszeit über die Fehlerverfolgungs-API bereitstellen. Es werden mehrere Fehler-IDs pro Sitzung unterstützt.

## So wird diese Dimension ausgefüllt

Der Player übergibt bei `media.error`-Ereignissen Fehler-IDs von Player-SDK an den Tracker. Das Backend erfasst eindeutige IDs über die gesamte Sitzung und meldet sie beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.playerSdkErrors`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoeplayersdkerrors, post_videoqoeplayersdkerrors` |

## Dimensionselemente

Jedes Element ist ein vom Player SDK generierter Fehler-Code oder eine ID. Verwenden Sie eine stabile Taxonomie für alle Implementierungen, damit Fehler-IDs sitzungsübergreifend korrekt aggregiert werden.
