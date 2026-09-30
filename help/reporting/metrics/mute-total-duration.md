---
title: Gesamtdauer der Stummschaltung
description: Gibt an, dass das kumulierte Audio in Sekunden während einer Sitzung stummgeschaltet wurde.
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
source-wordcount: '167'
ht-degree: 8%
---

# Gesamtdauer der Stummschaltung

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Gesamtdauer stummschalten**&#x200B;behandelt. Unter [Stummschaltung](/help/implementation/variables/player-state/mute.md) erfahren Sie, wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Metrik **Gesamtdauer stummschalten** zeigt die kumulative Zeit in Sekunden an, zu der das Audio während einer Sitzung stummgeschaltet wurde. Das Backend addiert jedes Intervall zwischen einem Stummschaltungs-Status-Start und dem entsprechenden Status-End-Ereignis.

## Berechnung dieser Metrik

Das Medien-Backend fasst die verstrichene Zeit in allen Stummschaltungsintervallen während der Sitzung zusammen. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.mute.time` wenn [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) aktiviert ist. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "mute"`, Feld `time` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.mute.time` |
