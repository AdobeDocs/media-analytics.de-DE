---
title: Staffel
description: Gibt die Saisonnummer für episodischen Inhalt an.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# Staffel

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsdimension **Staffel**behandelt. Siehe [Staffel](/help/implementation/variables/standard-metadata/season.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Dimension **Staffel** zeigt die Staffelnummer für episodischen Inhalt an. Verwenden Sie sie zusammen mit [Show](show.md) und [Episode](episode.md) für vollständige episodische Breakouts.

## So wird diese Dimension ausgefüllt

Die Staffel wird vom Player beim Sitzungsstart festgelegt, wenn der Inhalt Teil einer Serie ist.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.season`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Dimensionselemente

Jedes Element ist der literale Saisonwert, der beim Sitzungsstart gemeldet wird (in der Regel eine Zeichenfolgenganze wie `"1"`, `"2"`). Seien Sie über alle Folgen innerhalb derselben Sendung hinweg konsistent; die Dimension normalisiert `"1"` und `"01"` nicht auf denselben Zeileneintrag.
