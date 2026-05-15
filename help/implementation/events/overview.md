---
title: Übersicht über Streaming-Medienereignisse
description: Erfahren Sie mehr über Medienereignistypen und die Reihenfolge, in der sie gesendet werden müssen.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 4%

---


# Streaming-Medienereignisse

Die Nachverfolgung von Streaming-Medien funktioniert durch Senden einer Sequenz von Ereignisaufrufen, die jeweils eine Player-Statusübergabe darstellen, an einen Datenerfassungs-Endpunkt von Adobe. Jedes Ereignis gehört zu einer aktiven Sitzung, die mit einem [sessionStart](session/session-start.md)-Aufruf beginnt und mit [sessionComplete](session/session-complete.md) oder [sessionEnd](session/session-end.md) endet.

## Ereignis-Workflow

Die folgende sortierte Liste zeigt die erforderliche Ereignissequenz für eine typische VOD-Wiedergabe mit einer Pre-Roll-Anzeige und einem Kapitel:

1. **[Sitzungsstart](session/session-start.md)**: Immer das erste Ereignis; erstellt die Sitzung und gibt eine Sitzungs-ID zurück
2. **[Start der Werbeunterbrechung](ads/ad-break-start.md)**: Vor Anzeigenereignissen erforderlich
3. **[Anzeigenstart](ads/ad-start.md)** → **[Anzeige abgeschlossen](ads/ad-complete.md)** (oder **[Anzeigensprung](ads/ad-skip.md)**)
4. **[Werbeunterbrechung abgeschlossen](ads/ad-break-complete.md)**: Ist nach allen Anzeigen in der Unterbrechung erforderlich
5. **[Play](playback/play.md)**: Signalisiert den Beginn oder die Wiederaufnahme der Inhaltswiedergabe
6. **[Kapitelstart](chapters/chapter-start.md)**: Optional; markiert den Beginn eines Kapitels
7. **[Ping](playback/ping.md)**: Wird alle 10 Sekunden während des Hauptinhalts und alle 1 Sekunde während der Anzeigen gesendet
8. **[Kapitel abgeschlossen](chapters/chapter-complete.md)**: Optional; markiert das Ende eines Kapitels
9. **[Start anhalten](playback/pause-start.md)** → **[Play](playback/play.md)** (resume): Für jede Pause
10. **[Pufferstart](playback/buffer-start.md)** → **[Play](playback/play.md)** (resume): Für jede Pufferung
11. **[Sitzung abgeschlossen](session/session-complete.md)**: Wenn der Viewer das Ende des Inhalts erreicht

Verwenden Sie [Sitzungsende](session/session-end.md) anstelle von „Sitzung abgeschlossen“, wenn der Viewer die Sitzung abbricht, bevor das Ende des Inhalts erreicht ist.

## Sitzungslebenszyklus

Eine Sitzung läuft automatisch ab, wenn eine der folgenden Bedingungen erfüllt ist:

* Es werden keine Ereignisse für **10 Minuten empfangen**
* Keine Abspielkopfbewegung für **30 Minuten**

## Ereignisreferenz

| Ereignis | Kategorie | Zugeordnete Metrik |
| --- | --- | --- |
| [Sitzungsstart](session/session-start.md) | Sitzung | [Medienstarts](/help/reporting/metrics/media-starts.md) |
| [Sitzung abgeschlossen](session/session-complete.md) | Sitzung | [Inhalt abgeschlossen](/help/reporting/metrics/content-completes.md) |
| [Sitzungsende](session/session-end.md) | Sitzung | — |
| [Play](playback/play.md) | Wiedergabe | [Inhaltsstarts](/help/reporting/metrics/content-starts.md) |
| [Start anhalten](playback/pause-start.md) | Wiedergabe | [Ereignisse anhalten](/help/reporting/metrics/pause-events.md) |
| [Pufferstart](playback/buffer-start.md) | Wiedergabe | [Pufferereignisse](/help/reporting/metrics/buffer-events.md) |
| [Bitratenänderung](playback/bitrate-change.md) | Wiedergabe | [Bitratenänderungen](/help/reporting/metrics/bitrate-changes.md) |
| [Ping](playback/ping.md) | Wiedergabe | — |
| [Start der Werbeunterbrechung](ads/ad-break-start.md) | Werbeanzeigen | — |
| [Anzeigenstart](ads/ad-start.md) | Werbeanzeigen | [Anzeigenstarts](/help/reporting/metrics/ad-starts.md) |
| [Anzeige abgeschlossen](ads/ad-complete.md) | Werbeanzeigen | [Anzeige abgeschlossen](/help/reporting/metrics/ad-completes.md) |
| [Überspringen der Anzeige](ads/ad-skip.md) | Werbeanzeigen | — |
| [Werbeunterbrechung abgeschlossen](ads/ad-break-complete.md) | Werbeanzeigen | — |
| [Kapitelstart](chapters/chapter-start.md) | Kapitel | [Kapitelstarts](/help/reporting/metrics/chapter-starts.md) |
| [Kapitel abgeschlossen](chapters/chapter-complete.md) | Kapitel | [Kapitel abgeschlossen](/help/reporting/metrics/chapter-completes.md) |
| [Kapitelsprung](chapters/chapter-skip.md) | Kapitel | — |
| [Bundesland-Start](player-state/state-start.md) | Player-Status | Variiert je nach Status |
| [State-Ende](player-state/state-end.md) | Player-Status | Variiert je nach Status |
| [Fehler](error.md) | Qualität | [Von Fehlern betroffene Streams](/help/reporting/metrics/error-impacted-streams.md) |

>[!MORELIKETHIS]
>
>* [JSON-Validierungsschemata](/help/implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md): Überprüfen der Payload-Struktur der Anfrage für jeden Ereignistyp
>* [Ereignisanforderungs-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md): Endpunkt-Referenz zur Mediensammlungs-API
>* [Sitzungsanfrage-Endpunkt](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md): Erstellen einer Sitzung vor dem Senden von Ereignissen
>* [Player-Statusverfolgung](/help/use-cases/player-state-tracking/implementation-and-reporting.md): Details zum Status der Implementierung von Start und Ende
