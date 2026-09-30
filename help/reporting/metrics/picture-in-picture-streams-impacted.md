---
title: Von Bild in Bild betroffene Ströme
description: Zählt Sitzungen, in denen der Betrachter mindestens einmal Bild-in-Bild eingegeben hat.
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
source-wordcount: '192'
ht-degree: 7%
---

# Von Bild in Bild betroffene Ströme

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Von Bild in Bild betroffene Streams**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/picture-in-picture.md) unter „Bild in“.*

>[!ENDSHADEBOX]

Die Metrik **Von Bild in Bild betroffene Streams** zählt Sitzungen, in denen der Betrachter mindestens einmal an der Bild-in-Bild-Wiedergabe teilgenommen hat. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene. Es werden mehrere Bild-in-Bild-Einträge innerhalb derselben Sitzung gezählt, wie ein betroffener Stream. Verwenden Sie für die Gesamteingabemenge „Bild-in-Bild[&#x200B; „Bild-in-Bild-Anzahl](picture-in-picture-count.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten Empfang eines Bild-in-Bild-Status-Startereignisses während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.pictureinpicture.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "pictureInPicture"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
