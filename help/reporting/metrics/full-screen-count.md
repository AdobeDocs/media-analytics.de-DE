---
title: Anzahl der Vollbilder
description: Gibt an, wie oft der Viewer während einer Sitzung im Vollbildmodus angezeigt wurde.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# Anzahl der Vollbilder

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Vollbildanzahl**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/full-screen.md) im Vollbildmodus*

>[!ENDSHADEBOX]

Die Metrik **Anzahl des Vollbilds** gibt an, wie oft der Betrachter während einer Sitzung im Vollbildmodus angezeigt wurde. Bei jedem Vollbildstatus-Startereignis wird die Anzahl erhöht. Kombinieren Sie mit [Vom Vollbildmodus betroffene Streams](full-screen-streams-impacted.md) für boolesche Rollups auf Sitzungsebene und mit [Gesamtbilddauer](full-screen-total-duration.md) für die Gesamtzeit im Status.

## Berechnung dieser Metrik

Das Medien-Backend erhöht diese Anzahl bei jedem Status-Startereignis im Vollbildmodus. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.fullscreen.count` wenn [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "fullscreen"`, Feld `count` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
