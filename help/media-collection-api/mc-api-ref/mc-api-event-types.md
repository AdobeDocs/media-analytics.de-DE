---
seo-title: Ereignistypen und -beschreibungen
title: Ereignistypen und -beschreibungen
uuid: bc 4 f 75 a 7-ea 22-47 eb-a 50 d -5 f 41274 c 6 d 41
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Ereignistypen und -beschreibungen{#event-types-and-descriptions}

## sessionStart

Sent with the `sessions` call. Wenn die Antwort zurückgegeben wird, extrahieren Sie die Sitzungs-ID aus dem Location-Header und verwenden Sie sie für nachfolgende Aufrufe an den Sammlungsserver.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). Andere Status, von denen der Player zu „Playing“ wechseln kann, beinhalten „Buffering“ (Puffern), die Wiederaufnahme der Wiedergabe nach „Paused“ (Pause) oder Fehlermeldungen, die automatische Wiedergabe usw.

## ping

* **Hauptinhalt:** Muss während der Wiedergabe des Hauptinhalts unabhängig von anderen gesendeten API-Ereignissen alle zehn Sekunden gesendet werden. Der erste Ping sollte zehn Sekunden nach Beginn der Wiedergabe des Hauptinhalts ausgelöst werden.
* **Werbeinhalt:** Muss während des Anzeigen-Trackings jede Sekunde gesendet werden.

Ping-Ereignisse sollten *nicht* die `params`-Map im Anfrageinhalt enthalten.

## Bitratechange

Wird gesendet, wenn sich die Bitrage ändert.

## bufferStart

Wird gesendet, wenn Pufferung beginnt. Es gibt keinen Ereignistyp `bufferResume`. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

Wird gesendet, wenn der Benutzer auf Anhalten klickt. Es gibt keinen Ereignistyp `resume`. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

Signalisiert den Start einer Werbeunterbrechung

## adStart

Signalisiert den Start einer Anzeige

## adComplete

Signalisiert den Abschluss einer Werbeunterbrechung

## adSkip

Signalisiert, dass eine Anzeige übersprungen wird

## adBreakComplete

Signalisiert den Abschluss einer Werbeunterbrechung

## chapterStart

Signalisiert den Start eines Kapitelsegments

## chapterSkip

Signalisiert ein Kapitel überspringen

## chapterComplete

Signalisiert den Abschluss eines Kapitels

## error

Signalisiert einen Fehler.

## sessionEnd

Dies wird dazu verwendet, die Media Analytics-Sicherung zu benachrichtigen, um die Sitzung sofort zu schließen, wenn der Benutzer die Anzeige des Inhalts abgebrochen hat und er nicht zurückkehrt.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

Wird gesendet, wenn das Ende des Hauptinhalts erreicht wird.

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

