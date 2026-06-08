---
title: Versionshinweise zu Streaming Media Services
description: Versionshinweise für Streaming-Medien-Services anzeigen.
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
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 722
ht-degree: 36%

---

# Versionshinweise zu Streaming Media Services

**Letzte Aktualisierung**: 4. Juni 2026

## 2026

| Funktion | Beschreibung | Datum |
| --- | --- | --- |
| **Support-Zeitplandaten** | Hochladen geplanter Daten für vergangene Live-Inhalte, um die Zuschauerzahlen nach Programm oder Segment zu verfolgen. Zu den unterstützten Inhaltstypen gehören:<ul><li>FAST-Plattformen (Free Ad Supported TV)</li><li>Lokale Datenströme</li><li>Live-Sportübertragungen</li></ul>Weitere Informationen finden Sie [&#x200B; Anwendungsfall &#x200B;](/help/use-cases/track-schedule-data.md) Hochladen von Zeitplandaten zur Verfolgung von Live-Inhalten . | Rollout-Beginn: 29. Oktober 2025<p>Allgemeine Verfügbarkeit: Oktober 2026</p> |

## 2025

| Funktion | Beschreibung | Datum |
| --- | --- | --- |
| **`mediaTimed`veraltete XDM-Felder** | Das `mediaTimed` XDM-Objekt wird zugunsten von `mediaReporting` Feldpfaden nicht mehr unterstützt. Kunden, die den Analytics-Quell-Connector vor dem 9. Mai 2025 implementiert haben, müssen ihre Konfigurationen migrieren. Weitere Informationen finden Sie in den folgenden Migrationshandbüchern:<ul><li>[Migrieren von Zielgruppen zu den neuen Streaming-Medienfeldern](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[Migrieren Sie Customer Journey Analytics, um die neuen Streaming-Medienfelder zu verwenden](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[Migrieren der Datenvorbereitung für benutzerdefinierte Felder in die neuen Felder für Streaming-Medien](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[Migrieren von Profilen in die neuen Streaming-Medienfelder](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | Oktober 2025 |

## 2024

| Funktion | Beschreibung | Datum |
| --- | --- | --- |
| **Web SDK-Unterstützung** | Senden Sie Web-Daten von Streaming-Medien mit der Tag-Erweiterung Web SDK oder Web SDK an Adobe Experience Platform Edge Network und ermöglichen Sie so eine einheitliche Erfassungsmethode für alle Platform-Lösungen wie Customer Journey Analytics, Real-Time CDP, Journey Optimizer und Ereignisweiterleitung. Weitere Informationen [&#x200B; Sie unter „Einrichten der Web-SDK für Streaming](/help/implementation/edge/web-sdk.md)Medien“ oder [Einrichten der Tag-Erweiterung „Web](/help/implementation/edge/web-sdk-tags.md)SDK&quot; für Streaming-Medien. | &#x200B;29. Mai 2024 |
| **Roku-Unterstützung** | Senden Sie Streaming-Mediendaten mit dem Roku Edge SDK an Adobe Experience Platform. Weitere [&#x200B; finden Sie unter „Einrichten von Roku Edge für &#x200B;](/help/implementation/edge/roku.md) Media“. | &#x200B;12. April 2024 |

## 2023

| Funktion | Beschreibung | Datum |
| --- | --- | --- |
| **Experience Edge-Support** | Implementieren Sie die Streaming-Mediensammlung mit der Media Edge-API oder mit Mobile SDKs für iOS und Android.<ul><li>[Einrichten der Media Edge-API für Streaming-Medien](/help/implementation/edge/media-edge-api.md)</li><li>[Einrichten von iOS für Streaming](/help/implementation/edge/ios.md)Medien oder [Einrichten von iOS für Streaming-Medien mit Tags](/help/implementation/edge/ios-tags.md)</li><li>[Einrichten von Android für Streaming](/help/implementation/edge/android.md)Medien oder [Einrichten von Android für Streaming-Medien mit Tags](/help/implementation/edge/android-tags.md)</li></ul> | Samstag, 12. Mai 2023 |

## 2022

| Funktion | Beschreibung | Datum |
| --- | --- | --- |
| **Statusverfolgung für mehrere Player** | Verwenden Sie die Mediensammlungs-API, um die Statusverfolgung für mehrere [&#x200B; zu &#x200B;](/help/implementation/events/player-state/overview.md). | September 2022 |
| Umbenannte XDM-Felder | Umbenannte XDM-Feldnamen für Konsistenz:<ul><li>Audio- und Videoparameter</li><li>Anzeigenparameter</li><li>Kapitelparameter</li><li>Player-Statusparameter</li><li>Qualitätsparameter</li></ul> | September 2022 |
| **Zu Customer Journey Analytics hinzugefügte Bedienfelder** | Das Bedienfeld [Gleichzeitige Medienbetrachter](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) und [Bedienfeld „Mit Medienwiedergabe verbrachte Zeit“ wurde &#x200B;](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent) Customer Journey Analytics hinzugefügt. | &#x200B;9. August 2022 |
| **Zielgruppendurchschnitt pro Minute** | Sie können das Bedienfeld [Zielgruppendurchschnitt pro Minute](https://experienceleague.adobe.com/de/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel) verwenden, um die durchschnittliche Nutzung von Inhalten besser zu verstehen. <br>Der Zielgruppendurchschnitt pro Minute ermöglicht Vergleiche von Inhalten beliebiger Längen oder Genres. Darüber hinaus können Kunden diesen digitalen Zielgruppendurchschnitt pro Minute mit linearen Metriken zum TV-Durchschnitt pro Minute vergleichen oder ihn hinzufügen. Dieses Bedienfeld bietet mehr Flexibilität bei der Messung des Zielgruppendurchschnitts für benutzerdefinierte Zeiträume sowie für Fälle, bei denen die Klassifizierung der Dauer aktualisiert wurde. | &#x200B;16. März 2022 |

## 2021

| Funktion | Beschreibung | Datum |
| --- | --- | --- |
| **Bei Medienwiedergabe verbrachte Zeit** | Das [Panel „Wiedergabedauer](https://experienceleague.adobe.com/de/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent) bietet wertvolle Informationen zur Interaktion mit Betrachtern und ermöglicht es Medienunternehmen, tiefere, detailliertere Einblicke mit der minütigen Benutzerinteraktion durch erweiterte Zeitanalysen mit Tageszeiteneinteilungs-Funktionen zu gewinnen. Sie können feststellen, wie viel Zeit zu einem bestimmten Zeitpunkt mit der Anzeige Ihrer Medien-Streams verbracht wurde. Sie können die Wiedergabedauer nach verschiedenen Granularitäten unterteilen, einschließlich der neuen Granularitäten von 5, 15 und 30 Minuten. | September 2021 |

## 2020

| Funktion | Beschreibung | Datum |
| --- | --- | --- |
| **Bedienfeld „Gleichzeitige Medienbetrachter“** | Das [Bedienfeld „Gleichzeitige Betrachter](https://experienceleague.adobe.com/de/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers) hilft Ihnen zu verstehen, wo Spitzenzeiten von gleichzeitigen Ansichten auftraten oder wo es zu Abbrüchen kam. Erhalten Sie wertvolle Einblicke in die Qualität von Inhalten und die Interaktion mit Betrachtern und erhalten Sie Hilfe bei der Fehlerbehebung oder der Planung in Bezug auf Volumen und Skalierung.<br><br>[Bedienfeld „Gleichzeitige Medienbetrachter“ (Tutorial)](https://experienceleague.adobe.com/de/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | September 2020; Januar 2021 |
| **Unterstützte Geräte und Plattformen** | Die Media Launch-Erweiterung mit dem AEP-SDK unterstützt jetzt die folgenden OTT-Geräte: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Juni 2020 |
