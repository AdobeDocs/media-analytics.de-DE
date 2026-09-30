---
title: Anzahl der Anzeigen
description: Gibt die Anzahl der Anzeigen an, die während einer Sitzung gestartet wurden.
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
