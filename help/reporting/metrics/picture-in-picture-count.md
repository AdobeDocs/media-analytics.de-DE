---
title: Anzahl der Bilder im Bild
description: Gibt an, wie oft der Betrachter während einer Sitzung Bild-in-Bild eingegeben hat.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%
---

# Anzahl der Bilder im Bild

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Picture in Picture**) behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/picture-in-picture.md) unter „Bild in“.*

>[!ENDSHADEBOX]

Die Metrik **Anzahl der Bilder** gibt an, wie oft der Betrachter während einer Sitzung die Bild-in-Bild-Wiedergabe betreten hat. Jedes Bild-in-Bild-Status-Startereignis erhöht die Anzahl. Kombinieren Sie mit [Von Bild in Bild betroffene Streams](picture-in-picture-streams-impacted.md) für boolesche Rollups auf Sitzungsebene und mit [Gesamtdauer des Bildes in &#x200B;](picture-in-picture-total-duration.md) für die Gesamtzeit im Status.

## Berechnung dieser Metrik

Das Medien-Backend erhöht diese Anzahl bei jedem Bild-in-Bild-Status-Startereignis. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.pictureinpicture.count` wenn [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "pictureInPicture"`, Feld `count` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
