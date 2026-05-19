---
title: Versionshinweise zu Streaming Media Services
description: Versionshinweise für Streaming Media Services anzeigen.
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 1521
ht-degree: 82%

---

# Versionshinweise zu Streaming Media Services (Oktober 2025)

**Letztes Update**: Mittwoch, 7. Oktober 2025

## Verwandte Ressourcen

Informationen zu neuen Funktionen, Fehlerbehebungen und wichtige Informationen für Admins finden Sie in den folgenden Ressourcen.

* [Versionshinweise zu Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=de)
* [Versionshinweise zu Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=de)
* Die neuesten Versions-Updates für [Adobe Experience Cloud-Produkte](https://business.adobe.com/de/products/adobe-experience-cloud-products.html)

* [Adobe Analytics-Tutorials](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=de)

## *Aktuelle Versionshinweise*

## Neue und aktualisierte Funktionen für Adobe Streaming-Mediendienste {#cja-features}

| Funktion | Beschreibung | Zieldatum |
| ----------- | ---------- | ------- |
| **Streaming-Mediendienste: Unterstützung von Zeitplandaten** | Sie können jetzt Zeitplandaten von früheren Live-Inhalten von Streaming-Medien hochladen, um die Zuschauerzahlen einfacher und genauer zu verfolgen.<p>Im Folgenden finden Sie Beispiele für Live-Inhalte, die mit dem Upload von Zeitplandaten unterstützt werden:</p><ul><li>FAST-Plattformen (Free Ad Supported TV)</li><li>Lokale Datenströme</li><li>Live-Sportübertragungen</li></ul><p>Durch das Hochladen von Zeitplandaten können Sie die Zuschauerzahlen für einzelne Programme verfolgen, die in dem von Ihnen in der Upload-Datei angegebenen Zeitraum gelaufen sind. Sie können sogar Zuschauerzahlen für bestimmte Themen oder Programmsegmente erfassen.</p><p>Diese Funktionen sind unabhängig davon verfügbar, wie Sie die Erfassung von Streaming-Medien implementiert haben.</p><p>Zuvor war es bei der Analyse von Live-Inhalten schwierig, eine bestimmte Sitzung genau mit bestimmten Programmen zu verknüpfen, und es war nicht möglich, eine bestimmte Sitzung mit einzelnen Themen oder Programmsegmenten zu verknüpfen.</p><p>Weitere Informationen finden Sie unter [Hochladen von Zeitplandaten zum Nachverfolgen von Live-Inhalten](/help/use-cases/track-schedule-data.md)</p> | Rollout-Beginn: 29. Oktober 2025<p>Allgemeine Verfügbarkeit: Erste Jahreshälfte 2026</p><p>(Ursprünglich für die allgemeine Verfügbarkeit am 29. Oktober 2025 geplant)</p> |
| Aktualisierte XDM-Felder zum Erfassen von Streaming-Mediendaten in Adobe Experience Platform | Beim Erfassen von Streaming-Mediendaten in Adobe Experience Platform sollten die XDM-Feldpfade unter der Überschrift „XDM-Feldpfad“ in der Dokumentation zu den Streaming-Medienparametern nicht mehr verwendet werden. Stattdessen müssen Kundinnen und Kunden, die den Analytics-Quell-Connector vor dem 9. Mai 2025 implementiert haben, zum Erfassen von Streaming-Mediendaten in Platform ihre vorhandenen Konfigurationen in die mediaReporting-Feldpfade migrieren, wie unter der Überschrift „XDM-Feldpfad für Berichterstellung“ der Dokumentation zu Streaming-Medienparametern gezeigt.<p> Diese Feldpfade werden in den Variablenseiten für Streaming-Medien dokumentiert, die über die [Übersicht über Streaming-Medien-Services](../media-overview.md) verknüpft sind, und sind als „Veraltet“ gekennzeichnet. (Bei Kundinnen und Kunden, die den Analytics-Quell-Connector nach dem 9. Mai 2025 implementiert haben und bereits nur XDM-Pfade für mediaReporting verwenden, ist keine Aktion erforderlich.)</p><p>Die Datenaufnahme über die veralteten XDM-Feldpfade wird noch bis Ende Oktober 2025 fortgesetzt. Danach werden die veralteten Felder vollständig entfernt und nicht mehr in der Schema-Benutzeroberfläche von Adobe Experience Platform angezeigt. Daten werden nur mithilfe der mediaReporting-Feldpfade gesendet.</p><p>Weitere Informationen finden Sie unter [Migrieren einer Analytics-Quell-Connector-Implementierung zu aktualisierten XDM-Streaming-Medien-Feldern](/help/use-cases/xdm-updates/updated-xdm-fields.md).</p><p>Wenden Sie sich an Ihren Adobe Consulting-Dienst oder Ihr Konto-Team, um Unterstützung bei der Migration zu erhalten. </p> | Oktober 2025 |
| Senden von Web-Daten an Adobe Experience Platform Edge Network mit Web SDK | Sie können jetzt [Adobe Experience Platform Web SDK verwenden, um Web-Daten von Streaming-Medien an Adobe Experience Platform Edge Network zu senden](/help/implementation/edge/edge-web-sdk.md), sodass Sie stärker personalisierte Kampagnen erstellen und stärker personalisierte Inhalte bereitstellen können, was zu mehr Tracking-Daten führt, über die Berichte erstellt werden können.<p>Diese Erweiterung bietet eine einheitliche Erfassungsmethode für Web-Implementierungen über alle Platform-Lösungen hinweg, z. B. Customer Journey Analytics, RT-CDP, AJO und Ereignisweiterleitung. Zuvor bestand die einzige Möglichkeit, Web-Daten zu Streaming-Medien an Edge Network zu senden, in der Verwendung der Media Edge-API. | &#x200B;29. Mai 2024 |
| Roku-Daten an Adobe Experience Platform Edge senden | Wenn Sie [die Customer Journey Analytics Streaming Media Collection mit Experience Platform Edge installieren](/help/implementation/edge/implementation-edge.md) können Sie jetzt die Adobe Experience Platform Roku-SDK verwenden, um Streaming-Mediendaten an Adobe Experience Platform zu senden. | &#x200B;12. April 2024 |
| Mediensammlung: Integration mit Experience Edge (API und Mobile SDK) | Sie können jetzt die Experience Edge-API und Mobile SDK verwenden, um die Customer Journey Analytics-Streaming-Mediensammlung zu implementieren, sodass Sie stärker personalisierte Kampagnen erstellen und personalisierte Inhalte bereitstellen können, was zu mehr Tracking-Daten führt, über die Berichte erstellt werden können.<p>Diese Verbesserung bietet eine einheitliche Erfassungsmethode für alle Lösungen, z. B. Customer Journey Analytics-Reporting, RT-CDP, AJO und Ereignisweiterleitung.  [Weitere Informationen](/help/implementation/edge/implementation-edge.md) | Samstag, 12. Mai 2023 |
| Bedienfeld „Gleichzeitige Medienbetrachter“ | Erkennen Sie, wo hohe Auslastungen auftraten oder wo es zu Einbrüchen kam. Erhalten Sie wertvolle Einblicke in die Qualität von Inhalten und die Interaktion mit Betrachtern und erhalten Sie Hilfe bei der Fehlerbehebung oder der Planung in Bezug auf Volumen und Skalierung. [Weitere Informationen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=de) | &#x200B;9. August 2022 |
| Panel „Verbrachte Zeit bei der Medienwiedergabe“ | Die mit Medienwiedergabe verbrachte Zeit bietet wertvolle Einblicke in die Interaktion mit Betrachtenden und ermöglicht es Medienunternehmen, tiefere, detailliertere Einblicke mit der minütigen Benutzerinteraktion durch erweiterte Zeitanalysen mit Funktionen zur Tageszeiteneinteilung zu gewinnen. Sie können feststellen, wie viel Zeit zu einem bestimmten Zeitpunkt mit der Anzeige Ihrer Medien-Streams verbracht wurde. Sie können die Wiedergabedauer nach verschiedenen Granularitäten aufteilen, einschließlich der neuen Granularitäten 5 Minuten, 15 Minuten und 30 Minuten. [Weitere Informationen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=de) | &#x200B;9. August 2022 |
| Freigeben von Anmerkungen in mobilen Scorecards | Sie können in Workspace erstellte Anmerkungen in mobilen Scorecards anzeigen. Auf diese Weise können Sie kontextbezogene Datennuancen und Erkenntnisse zu Ihrer Organisation und Ihren Kampagnen direkt in Projekten mit mobiler Scorecard, die in der Dashboard-Mobile-App von Analytics angezeigt werden. [Weitere Informationen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=de) | &#x200B;15. Juni 2022 |
| Updates für Report Builder für Customer Journey Analytics | Enthält Funktionen wie Planung und Datenblock-Manager. [Weitere Informationen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=de) | &#x200B;18. Mai 2022 |
| Anmerkungen in Analysis Workspace | Mit Anmerkungen in Analysis Workspace können Sie Ihrer Organisation kontextbezogene Informationen und Einblicke zu Daten effektiv übermitteln. [Weitere Informationen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=de) | Der schrittweise Rollout beginnt am 23. März 2022 |
| Vorschaumodus für Mobile Scorecard-Projekte | Starten Sie direkt im Scorecard-Builder eine Vorschau Ihrer Mobile Scorecard, um zu sehen, wie sie in der Mobile App von Analytics-Dashboards aussehen wird. Im Vorschaumodus können Benutzer auf die gleiche Weise mit Filtern und Diagrammen interagieren wie in der Mobile App, sodass sie eine Vorschau des Erlebnisses erhalten, bevor sie die Scorecard speichern und freigeben. Benutzer können im Vorschaumodus auch die Geräteauswahl verwenden, um zu sehen, wie ihre Scorecard auf verschiedenen Geräten aussieht. [Weitere Informationen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=de#preview) | &#x200B;16. Februar 2022 |


## Neue und aktualisierte Funktionen für Adobe Streaming-Mediendienste {#sm-features}

| Funktion | Beschreibung | Zieldatum |
| ----------- | ---------- | ------- |
| Statusverfolgung für mehrere Player | Verwenden Sie die Mediensammlungs-API, um die Statusverfolgung für mehrere Player zu implementieren. [Weitere Informationen](/help/use-cases/player-state-tracking/multiple-player-states.md) | September 2022 |
| Umbenannte XDM-Felder | Umbenannte XDM-Feldnamen für Konsistenz:<br>* Audio- und Videoparameter<br>* Anzeigenparameter<br>* Kapitelparameter<br>* Player-Statusparameter<br>* Qualitätsparameter | September 2022 |
| Verweis auf Geräte-Kooperation | Der Verweis auf die Adobe Experience Cloud-Gerätekooperation und die Erfordernis des ID-Services von Experience Cloud wurde entfernt. | August 2022 |
| Aktualisierte Feldnamen und XDM-Pfade für die Sammlung und Berichterstellung | Folgendes wurde aktualisiert:<br>* Audio- und Videoparameter<br>* Anzeigenparameter<br>* Kapitelparameter<br>* Player-Statusparameter<br>* Qualitätsparameter | August 2022 |
| Zielgruppendurchschnitt pro Minute | Media Analytics-Kunden können das Bedienfeld „Zielgruppendurchschnitt pro Minute“ verwenden, um die durchschnittliche Nutzung ihrer Inhalte besser zu verstehen. <br>Der Zielgruppendurchschnitt pro Minute ermöglicht Vergleiche von Inhalten beliebiger Längen oder Genres. Darüber hinaus können Kunden diesen digitalen Zielgruppendurchschnitt pro Minute mit linearen Metriken zum TV-Durchschnitt pro Minute vergleichen oder ihn hinzufügen. Dieses Bedienfeld bietet mehr Flexibilität bei der Messung des Zielgruppendurchschnitts für benutzerdefinierte Zeiträume sowie für Fälle, bei denen die Klassifizierung der Dauer aktualisiert wurde.  [Weitere Informationen](/help/reporting/workspace/average-minute-audience.md) | &#x200B;16. März 2022 |
| Bedienfeld „Mit Medienwiedergabe verbrachte Zeit“ | Erfahren Sie, wie das Bedienfeld „Mit Medienwiedergabe verbrachte Zeit“ es Medienbenutzern ermöglicht, ihre Zuschauerzahlen anhand der während eines Tages mit Ansehen verbrachten Zeit in einer gewählten Granularität zu verstehen. <br>[Bedienfeld „Bei Medienwiedergabe verbrachte Zeit“ (Tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=de) | Januar 2022 |


## *Frühere Versionshinweise*

| Funktion | Beschreibung | Targeting- oder Aktualisierungsdatum |
| ----------- | ---------- | -------------- |
| Bei Medienwiedergabe verbrachte Zeit | Die mit Adobe Streaming-Medienwiedergabe verbrachte Zeit bietet wertvolle Einblicke in die Interaktion mit Betrachtern und ermöglicht es Medienunternehmen, durch erweiterte Zeitanalysen mit Tageszeiteneinteilungs-Funktionen tiefere, minutengenaue Einblicke in die Benutzerinteraktion zu gewinnen. Sie können feststellen, wie viel Zeit zu einem bestimmten Zeitpunkt mit der Anzeige Ihrer Medien-Streams verbracht wurde. Sie können die Wiedergabedauer nach verschiedenen Granularitäten unterteilen, einschließlich der neuen Granularitäten von 5, 15 und 30 Minuten. [Weitere Informationen...](/help/reporting/workspace/media-playback-time-spent.md) | September 2021 |
| Bedienfeld „Gleichzeitige Medienbetrachter“ in Analytics Workspace | Erkennen Sie, wo hohe Auslastungen auftraten oder wo es zu Einbrüchen kam. Erhalten Sie wertvolle Einblicke in die Qualität von Inhalten und die Interaktion mit Betrachtern und erhalten Sie Hilfe bei der Fehlerbehebung oder der Planung in Bezug auf Volumen und Skalierung. [Weitere Informationen...](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Bedienfeld „Gleichzeitige Medienbetrachter“ in Analytics Workspace (Tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=de#analysis-workspace) | September 2020 <br><br><br>Januar 2021 |
| Unterstützte Geräte und Plattformen | Die Media Launch-Erweiterung mit dem AEP-SDK unterstützt jetzt die folgenden OTT-Geräte: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Juni 2020 |


<!--
## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | 
-->
