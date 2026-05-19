---
title: Von Bild in Bild betroffene Ströme
description: Zählt Sitzungen, in denen der Betrachter mindestens einmal Bild-in-Bild eingegeben hat.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---


# Von Bild in Bild betroffene Ströme

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Von Bild in Bild betroffene Streams**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/picture-in-picture.md) unter „Bild in“.*

>[!ENDSHADEBOX]

Die Metrik **Von Bild in Bild betroffene Streams** zählt Sitzungen, in denen der Betrachter mindestens einmal an der Bild-in-Bild-Wiedergabe teilgenommen hat. Bei der Metrik handelt es sich um einen booleschen Wert auf Sitzungsebene - mehrere Bild-in-Bild-Einträge innerhalb derselben Sitzungsanzahl wie ein betroffener Stream. Verwenden Sie für die Gesamteingabemenge „Bild-in-Bild[&#x200B; „Bild-in-Bild-Anzahl](picture-in-picture-count.md).

## Berechnung dieser Metrik

Das Medien-Backend setzt dieses Flag beim ersten Empfang eines Bild-in-Bild-Status-Startereignisses während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.pictureinpicture.set` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "pictureInPicture"`, Feld `isSet` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
