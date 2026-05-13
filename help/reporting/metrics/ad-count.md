---
title: Anzahl der Anzeigen
description: Gibt die Anzahl der Anzeigen an, die während einer Sitzung gestartet wurden.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Anzahl der Anzeigen

Die Metrik **Anzeigenanzahl** gibt die Anzahl der Anzeigen an, die während einer Sitzung gestartet wurden. Verwenden Sie sie, um Inhalt, Kanal oder Stream-Typ zu verstehen und nach Inhalt zu laden. Für Anzeigenstartzahlen, die nach Anzeigendimensionen (Advertiser, Kampagne, Kreative) gedreht werden, verwenden Sie die Metrik Anzeigenstarts , die verfügbar ist, wenn die Variablenkategorie „Anzeigen“ aktiviert ist.

## Berechnung dieser Metrik

Das Medien-Backend erhöht `mediaReporting.sessionDetails.adCount` bei jedem während der Sitzung empfangenen `media.adStart`. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.adCount` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.adCount`; siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
