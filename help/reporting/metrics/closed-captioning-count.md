---
title: Anzahl der verdeckten Untertitel
description: Gibt an, wie oft der Viewer Untertitel während einer Sitzung aktiviert hat.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---


# Anzahl der verdeckten Untertitel

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Geschlossene Untertitelanzahl**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/player-state/closed-captioning.md) unter „Untertitel“*

>[!ENDSHADEBOX]

Die Metrik **Geschlossene Untertitel** gibt an, wie oft der Viewer Untertitel während einer Sitzung aktiviert hat. Jedes Startereignis, bei dem der Untertitelstatus aktiviert wird, erhöht die Anzahl. Kombinieren Sie mit [Von geschlossenen Untertiteln betroffene Streams](closed-captioning-streams-impacted.md) für boolesche Rollups auf Sitzungsebene und mit [Gesamtdauer für geschlossene ](closed-captioning-total-duration.md) für die Gesamtzeit im Status .

## Berechnung dieser Metrik

Das Medien-Backend erhöht diese Anzahl bei jedem Startereignis für den Untertitelaktivierungsstatus. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.closedcaptioning.count` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "closedCaptioning"`, Feld `count` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.count` |
