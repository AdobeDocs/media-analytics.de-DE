---
title: Gesamtdauer des Bilds im Bild
description: Gibt die kumulierten Sekunden an, die der Betrachter während einer Sitzung im Bild-in-Bild verbracht hat.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 7%

---


# Gesamtdauer des Bilds im Bild

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Gesamtdauer des Bildes**behandelt. Informationen [ Erfassen dieser Variablen finden ](/help/implementation/variables/player-state/picture-in-picture.md) unter „Bild in“.*

>[!ENDSHADEBOX]

Die Metrik **Gesamtdauer des Bildes** gibt die kumulative Zeit in Sekunden an, die der Viewer während einer Sitzung im Bild-in-Bild verbracht hat. Das Backend addiert jedes Intervall zwischen einem Bild-in-Bild-Status-Start und dem passenden Status-End-Ereignis.

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Zeit über alle Bild-in-Bild-Intervalle während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.pictureinpicture.time` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "pictureInPicture"`, Feld `time` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.time` |
