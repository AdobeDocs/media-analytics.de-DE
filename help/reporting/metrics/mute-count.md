---
title: Anzahl stummschalten
description: Gibt an, wie oft der Viewer Audio während einer Sitzung stummgeschaltet hat.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---


# Anzahl stummschalten

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Stummschaltungszählungen**&#x200B;behandelt. Unter [Stummschaltung](/help/implementation/variables/player-state/mute.md) erfahren Sie, wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Metrik **Zählung der Stummschaltung** gibt an, wie oft der Viewer Audio während einer Sitzung stummgeschaltet hat. Bei jedem Startereignis mit Stummschaltung wird die Anzahl erhöht. Kombinieren Sie mit [Von Stummschaltung betroffene Streams](mute-streams-impacted.md) für boolesche Rollups auf Sitzungsebene und mit [Gesamtdauer Stummschalten](mute-total-duration.md) für die Gesamtzeit im Status.

## Berechnung dieser Metrik

Das Medien-Backend erhöht das Feld `count` im `mute` von `mediaReporting.states[]` bei jedem Startereignis mit stummgeschaltetem Zustand. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.mute.count` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "mute"`, Feld `count` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
