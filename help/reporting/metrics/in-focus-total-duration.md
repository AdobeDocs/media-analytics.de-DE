---
title: Gesamtdauer des Fokus
description: Gibt die kumulierten Sekunden an, die der Player während einer Sitzung im Fokus war.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---


# Gesamtdauer des Fokus

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Gesamtdauer des Fokus**behandelt. Siehe [Im Fokus](/help/implementation/variables/player-state/in-focus.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Metrik **Gesamtdauer des Fokus** gibt die kumulative Zeit in Sekunden an, während der der Player während einer Sitzung im Fokus war. Das Backend addiert jedes Intervall zwischen einem Fokusstatus-Start und dem passenden Statusend-Ereignis.

## Berechnung dieser Metrik

Das Medien-Backend fasst die verstrichene Zeit in allen Fokusintervallen während der Sitzung zusammen. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.infocus.time` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "inFocus"`, Feld `time` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.infocus.time` |
