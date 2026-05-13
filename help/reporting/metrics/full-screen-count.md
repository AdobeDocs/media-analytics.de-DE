---
title: Anzahl der Vollbilder
description: Gibt an, wie oft der Viewer während einer Sitzung im Vollbildmodus angezeigt wurde.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 7%

---


# Anzahl der Vollbilder

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Vollbildanzahl**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/player-state/full-screen.md) im Vollbildmodus*

>[!ENDSHADEBOX]

Die Metrik **Anzahl des Vollbilds** gibt an, wie oft der Betrachter während einer Sitzung im Vollbildmodus angezeigt wurde. Bei jedem Vollbildstatus-Startereignis wird die Anzahl erhöht. Kombinieren Sie mit [Vom Vollbildmodus betroffene Streams](full-screen-streams-impacted.md) für boolesche Rollups auf Sitzungsebene und mit [Gesamtbilddauer](full-screen-total-duration.md) für die Gesamtzeit im Status.

## Berechnung dieser Metrik

Das Medien-Backend erhöht das Feld `count` im `fullscreen` Eintrag von `mediaReporting.states[]` bei jedem Start-Ereignis im Vollbildmodus. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.fullscreen.count` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "fullscreen"`, Feld `count` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
