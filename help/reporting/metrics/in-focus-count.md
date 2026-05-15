---
title: Anzahl der Fokussierungen
description: Gibt an, wie oft der Player während einer Sitzung den Fokus erhalten hat.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# Anzahl der Fokussierungen

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Anzahl der**&quot; behandelt. Siehe [Im Fokus](/help/implementation/variables/player-state/in-focus.md), wie Sie diese Variable erfassen.*

>[!ENDSHADEBOX]

Die Metrik **Anzahl der Fokussierungen** gibt an, wie oft der Player während einer Sitzung den Fokus erhalten hat. Bei jedem Fokusstatus-Startereignis wird die Anzahl erhöht. Kombinieren Sie mit [Von im Fokus betroffene Streams](in-focus-streams-impacted.md) für boolesche Rollups auf Sitzungsebene und mit [Gesamtdauer des Fokus](in-focus-total-duration.md) für die Gesamtzeit im Status.

## Berechnung dieser Metrik

Das Medien-Backend erhöht das Feld `count` in der `inFocus` Eingabe von `mediaReporting.states[]` bei jedem Fokusstatus-Startereignis. Die Metrik wird beim Schließen-Aufruf gemeldet.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.infocus.count` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/de/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "inFocus"`, Feld `count` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/de/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
