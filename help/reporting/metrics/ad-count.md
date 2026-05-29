---
title: Anzahl der Anzeigen
description: Gibt die Anzahl der Anzeigen an, die während einer Sitzung gestartet wurden.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 9%

---


# Anzahl der Anzeigen

Die Metrik **Anzeigenanzahl** gibt die Anzahl der Anzeigen an, die während einer Sitzung gestartet wurden. Verwenden Sie sie, um Inhalt, Kanal oder Stream-Typ zu verstehen und nach Inhalt zu laden. Für Anzeigenstartzahlen, die nach Anzeigendimensionen (Advertiser, Kampagne, Kreative) gedreht werden, verwenden Sie die Metrik Anzeigenstarts , die verfügbar ist, wenn die Variablenkategorie „Anzeigen“ aktiviert ist.

## Berechnung dieser Metrik

Das Medien-Backend erhöht diese Anzahl bei jedem [Anzeigenstart](/help/implementation/events/ads/ad-start.md)-Ereignis, das während der Sitzung empfangen wurde. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Erstellen Sie [Verarbeitungsregel](https://experienceleague.adobe.com/de/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) die `a.media.adCount` einem benutzerdefinierten Ereignis zuordnet. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (das benutzerdefinierte Ereignis, dem Ihre Verarbeitungsregel zugeordnet `a.media.adCount`; siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | nicht angegeben |
