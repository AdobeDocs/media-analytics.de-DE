---
title: Gesamtdauer des Bilds im Bild
description: Gibt die kumulierten Sekunden an, die der Betrachter während einer Sitzung im Bild-in-Bild verbracht hat.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 6%

---


# Gesamtdauer des Bilds im Bild

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Berichtsmetrik **Gesamtdauer des Bildes**&#x200B;behandelt. Informationen [&#x200B; Erfassen dieser Variablen finden &#x200B;](/help/implementation/variables/player-state/picture-in-picture.md) unter „Bild in“.*

>[!ENDSHADEBOX]

Die Metrik **Gesamtdauer des Bildes** gibt die kumulative Zeit in Sekunden an, die der Viewer während einer Sitzung im Bild-in-Bild verbracht hat. Das Backend addiert jedes Intervall zwischen einem Bild-in-Bild-Status-Start und dem passenden Status-End-Ereignis.

## Berechnung dieser Metrik

Das Medien-Backend addiert die verstrichene Zeit über alle Bild-in-Bild-Intervalle während der Sitzung. Die Metrik wird beim Schließen-Aufruf gemeldet. Analysis Workspace zeigt den Wert als `HH:MM:SS` an; Daten-Feeds, Data Warehouse und Reporting-APIs zeigen den Wert in Sekunden an.

| Meldesystem | Quelle |
| --- | --- |
| Adobe Analytics | Wird automatisch aus dem Kontextdatenmodell erfasst`a.media.states.pictureinpicture.time` wenn [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) aktiviert ist. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) Eintrag, bei dem `name = "pictureInPicture"`, Feld `time` |
| Daten-Feeds | `event_list`, `post_event_list` (siehe [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) Suche) |
