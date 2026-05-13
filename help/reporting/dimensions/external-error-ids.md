---
title: Externe Fehler-IDs
description: Meldet eindeutige Fehlerkennungen aus externen Quellen, z. B. CDN-Fehler.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# Externe Fehler-IDs

Die Dimension **Externe Fehler** IDs) meldet eindeutige Fehlerkennungen aus allen Quellen außerhalb der Player-SDK (z. B. CDN-Fehler). Der Player muss die Codes oder IDs zur Implementierungszeit über die Fehlerverfolgungs-API bereitstellen. Es werden mehrere Fehler-IDs pro Sitzung unterstützt.

## So wird diese Dimension ausgefüllt

Bei `media.error` Ereignissen übergibt der Player externe Fehler-IDs an den Tracker. Das Backend erfasst eindeutige IDs über die gesamte Sitzung und meldet sie beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.externalErrors`, wenn [[!UICONTROL Medienqualität]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoeextneralerrors` |

## Dimensionselemente

Jedes Element ist ein Fehler-Code oder eine ID, die vom Player bereitgestellt wird. Verwenden Sie eine stabile Taxonomie für alle Implementierungen, damit Fehler-IDs sitzungsübergreifend korrekt aggregiert werden.
