---
title: Externe Fehler-IDs
description: Meldet eindeutige Fehlerkennungen aus externen Quellen, z. B. CDN-Fehler.
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
source-wordcount: '155'
ht-degree: 7%
---

# Externe Fehler-IDs

Die Dimension **Externe Fehler** IDs) meldet eindeutige Fehlerkennungen aus allen Quellen außerhalb der Player-SDK (z. B. CDN-Fehler). Der Player muss die Codes oder IDs zur Implementierungszeit über die Fehlerverfolgungs-API bereitstellen. Es werden mehrere Fehler-IDs pro Sitzung unterstützt.

## So wird diese Dimension ausgefüllt

Der Player übergibt bei Ereignissen des Typs &quot;[&quot; externe Fehler](/help/implementation/events/error.md)IDs an den Tracker. Das Backend erfasst eindeutige IDs über die gesamte Sitzung und meldet sie beim Schließen-Aufruf.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.qoe.externalErrors`, wenn [[!UICONTROL Medienqualität]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Daten-Feeds | `videoqoeextneralerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.externalErrors` |

## Dimensionselemente

Jedes Element ist ein Fehler-Code oder eine ID, die vom Player bereitgestellt wird. Verwenden Sie eine stabile Taxonomie für alle Implementierungen, damit Fehler-IDs sitzungsübergreifend korrekt aggregiert werden.
