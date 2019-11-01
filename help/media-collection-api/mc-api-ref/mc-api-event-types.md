---
title: Ereignistypen und -beschreibungen
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Ereignistypen und -beschreibungen{#event-types-and-descriptions}

## sessionStart

Gesendet mit dem `sessions` Anruf. Wenn die Antwort zurückgegeben wird, extrahieren Sie die Sitzungs-ID aus dem Location-Header und verwenden Sie sie für nachfolgende Aufrufe an den Sammlungsserver.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). Andere Status, von denen der Player zu „Playing“ wechseln kann, beinhalten „Buffering“ (Puffern), die Wiederaufnahme der Wiedergabe nach „Paused“ (Pause) oder Fehlermeldungen, die automatische Wiedergabe usw.

## ping

* **Hauptinhalt:** Muss während der Wiedergabe des Hauptinhalts unabhängig von anderen gesendeten API-Ereignissen alle zehn Sekunden gesendet werden. Der erste Ping sollte zehn Sekunden nach Beginn der Wiedergabe des Hauptinhalts ausgelöst werden.
* **Werbeinhalt:** Muss während des Anzeigen-Trackings jede Sekunde gesendet werden.

Ping-Ereignisse sollten *nicht* die `params`-Map im Anfrageinhalt enthalten.

## bitrateChange

Wird gesendet, wenn sich die Bitrate ändert.

## bufferStart

Wird gesendet, wenn die Pufferung beginnt. Es gibt keinen Ereignistyp `bufferResume`. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

Wird gesendet, wenn der Benutzer Pause drückt. Es gibt keinen Ereignistyp `resume`. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

Gibt den Beginn einer Werbeunterbrechung an

## adStart

Gibt den Beginn einer Anzeige an

## adComplete

Gibt den Abschluss einer Werbeunterbrechung an

## adSkip

Signiert eine übersprungene Anzeige

## adBreakComplete

Gibt den Abschluss einer Werbeunterbrechung an

## chapterStart

Gibt den Beginn eines Kapitelsegments an

## chapterSkip

Signiert eine Kapitelüberspringe

## chapterComplete

Gibt den Abschluss eines Kapitels an

## error

Gibt einen Fehler an.

## sessionEnd

Dadurch wird das Media Analytics-Back-End benachrichtigt, dass die Sitzung sofort geschlossen wird, wenn der Benutzer die Anzeige des Inhalts abgebrochen hat und wahrscheinlich keine Rückkehr erfolgt.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

Wird gesendet, wenn das Ende des Hauptinhalts erreicht wird

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

