---
title: Autorisiert
description: Zählt Sitzungen, deren Benutzer über Adobe Pass autorisiert wurden.
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
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell `a.media.pass.auth`, wenn [[!UICONTROL Videometadaten]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
