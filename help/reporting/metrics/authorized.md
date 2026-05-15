---
title: Autorisiert
description: Zählt Sitzungen, deren Benutzer über Adobe Pass autorisiert wurden.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 12%

---


# Autorisiert

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Autorisiert**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/standard-metadata/authorized.md) unter „Autorisiert“*

>[!ENDSHADEBOX]

Die Metrik **Autorisiert** zählt Sitzungen, deren Benutzer über Adobe Pass oder TV-Everywhere autorisiert wurden. Kombinieren Sie mit der Dimension [MVPD](/help/reporting/dimensions/mvpd.md), um das Authentifizierungsvolumen nach Anbieter aufzuschlüsseln.

## Berechnung dieser Metrik

Das Medien-Backend erhöht die Anzahl, wenn der Player die Sitzung beim Sitzungsstart als autorisiert kennzeichnet. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pass.auth`, wenn [[!UICONTROL Videometadaten]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
