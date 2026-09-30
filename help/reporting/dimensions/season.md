---
title: Staffel
description: Gibt die Saisonnummer für episodischen Inhalt an.
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
source-wordcount: '140'
ht-degree: 11%
---

# Staffel

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Staffel**&#x200B;behandelt. Siehe [Staffel](/help/implementation/variables/standard-metadata/season.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Staffel** zeigt die Staffelnummer für episodischen Inhalt an. Verwenden Sie sie zusammen mit [Show](show.md) und [Episode](episode.md) für vollständige episodische Breakouts.

## So wird diese Dimension ausgefüllt

Die Staffel wird vom Player beim Sitzungsstart festgelegt, wenn der Inhalt Teil einer Serie ist.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.season`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Dimensionselemente

Jedes Element ist der literale Saisonwert, der beim Sitzungsstart gemeldet wird (in der Regel eine Zeichenfolgenganze wie `"1"`, `"2"`). Seien Sie über alle Folgen innerhalb derselben Sendung hinweg konsistent; die Dimension normalisiert `"1"` und `"01"` nicht auf denselben Zeileneintrag.
