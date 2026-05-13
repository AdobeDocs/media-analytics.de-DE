---
title: Gesamtdauer im Vollbildmodus
description: Gibt die kumulierten Sekunden an, die der Betrachter während einer Sitzung im Vollbildmodus verbracht hat.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# Gesamtdauer im Vollbildmodus

>[!BEGINSHADEBOX]

*Diese Seite deckt die Berichtsmetrik **Gesamtdauer im Vollbildmodus**&#x200B;ab. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/full-screen.md) im Vollbildmodus*

>[!ENDSHADEBOX]

Die Metrik **Gesamtdauer im Vollbildmodus** zeigt die kumulative Zeit in Sekunden an, die der Betrachter während einer Sitzung im Vollbildmodus verbracht hat. Das Backend addiert jedes Intervall zwischen einem Vollbildstatus-Start und dem passenden Statusend-Ereignis.

## Berechnung dieser Metrik

Das Medien-Backend fasst die verstrichene Zeit in allen Vollbildintervallen während der Sitzung zusammen. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.fullscreen.time` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "fullscreen"`, Feld `time` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
