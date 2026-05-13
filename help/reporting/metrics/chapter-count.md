---
title: Anzahl der Kapitel
description: Gibt die Anzahl der Kapitel an, die während einer Sitzung begonnen haben.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---


# Anzahl der Kapitel

Die Metrik **Kapitelanzahl** gibt die Anzahl der Kapitel an, die während einer Sitzung begonnen haben. Verwenden Sie sie, um die Kapitelnutzung über Inhalte hinweg zu vergleichen. Für Kapitelstartzahlen, die um Kapiteldimensionen (Kapitelname, Position) gedreht wurden, verwenden Sie die Metrik Kapitelstarts , die verfügbar ist, wenn die Kategorie der Variablen „Kapitel“ aktiviert ist.

## Berechnung dieser Metrik

Das Medien-Backend erhöht `mediaReporting.sessionDetails.chapterCount` bei jedem während der Sitzung empfangenen `media.chapterStart`. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.chapterCount` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.chapterCount`; siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
