---
title: Gesamtdauer für verdeckte Untertitel
description: meldet die Aktivierung der kumulierten Sekundenbeschriftungen während einer Sitzung.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 7%

---


# Gesamtdauer für verdeckte Untertitel

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Gesamtdauer für Untertitel**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/closed-captioning.md) unter „Untertitel“*

>[!ENDSHADEBOX]

Die Metrik **Gesamtdauer für Untertitel** gibt die kumulative Zeit in Sekunden an, zu der die Untertitel während einer Sitzung aktiviert wurden. Das Backend addiert jedes Intervall zwischen dem Start des Untertitelaktivierungsstatus und dem entsprechenden Statusendereignis.

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Zeit in allen Untertitelintervallen während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.closedcaptioning.time` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "closedCaptioning"`, Feld `time` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
