---
title: Anzahl der Bilder im Bild
description: Gibt an, wie oft der Betrachter während einer Sitzung Bild-in-Bild eingegeben hat.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 7%

---


# Anzahl der Bilder im Bild

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Picture in Picture**) behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/player-state/picture-in-picture.md) unter „Bild in“.*

>[!ENDSHADEBOX]

Die Metrik **Anzahl der Bilder** gibt an, wie oft der Betrachter während einer Sitzung die Bild-in-Bild-Wiedergabe betreten hat. Jedes Bild-in-Bild-Status-Startereignis erhöht die Anzahl. Kombinieren Sie mit [Von Bild in Bild betroffene Streams](picture-in-picture-streams-impacted.md) für boolesche Rollups auf Sitzungsebene und mit [Gesamtdauer des Bildes in ](picture-in-picture-total-duration.md) für die Gesamtzeit im Status.

## Berechnung dieser Metrik

Das Medien-Backend erhöht das `count` in der `pictureInPicture` Eingabe von `mediaReporting.states[]` bei jedem Bild-in-Bild-Status-Startereignis. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.pictureinpicture.count` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "pictureInPicture"`, Feld `count` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
