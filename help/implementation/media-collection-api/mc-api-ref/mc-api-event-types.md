---
title: Ereignistypen und -beschreibungen für Streaming-Medien
description: 'Was sind die Ereignistypen und -beschreibungen der Mediensammlung? '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 98722998606af3761652e282c31338bb966eb654
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 79%

---

# Ereignistypen und -beschreibungen{#event-types-and-descriptions}

## sessionStart

Wird mit dem `sessions`-Aufruf gesendet. Wenn die Antwort zurückgegeben wird, extrahieren Sie die Sitzungs-ID aus dem Location-Header und verwenden Sie sie für nachfolgende Aufrufe an den Sammlungsserver.

## play

Wird gesendet, wenn der Player den Status zu „Playing“ (Wiedergabe) ändert (z. B. wenn der `on('Playing')`-Callback vom Player ausgelöst wird). Andere Status, von denen der Player zu „Playing“ wechseln kann, beinhalten „Buffering“ (Puffern), die Wiederaufnahme der Wiedergabe nach „Paused“ (Pause) oder Fehlermeldungen, die automatische Wiedergabe usw.

## ping

* **Hauptinhalt -** Muss während der Wiedergabe des Hauptinhalts unabhängig von anderen gesendeten API-Ereignissen alle zehn Sekunden gesendet werden. Das erste Ping-Ereignis sollte 10 Sekunden nach Beginn der Wiedergabe des Hauptinhalts ausgelöst werden.
* **Anzeigeninhalt -** Muss während dem Anzeigen-Tracking jede Sekunde gesendet werden.

Ping-Ereignisse sollten *nicht* die `params`-Map im Anfrageinhalt enthalten.

## bitrateChange

Wird gesendet, wenn sich die Bitrate ändert.

## bufferStart

Wird gesendet, wenn ein Puffervorgang beginnt. Es gibt keinen Ereignistyp `bufferResume`. `bufferResume` wird erkannt, wenn Sie ein `play`-Ereignis nach `bufferStart` senden.

## pauseStart

Wird gesendet, wenn der Benutzer die Wiedergabe anhält. Es gibt keinen Ereignistyp `resume`. `resume` wird erkannt, wenn Sie ein `play`-Ereignis nach `pauseStart` senden.

## adBreakStart

Signalisiert den Start einer Werbeunterbrechung.

## adStart

Signalisiert den Start einer Werbeanzeige.

## adComplete

Signalisiert den Abschluss einer Werbeunterbrechung.

## adSkip

Signalisiert das Überspringen einer Werbeanzeige.

## adBreakComplete

Signalisiert den Abschluss einer Werbeunterbrechung.

## chapterStart

Signalisiert den Start eines Kapitelsegments.

## chapterSkip

Signalisiert das Überspringen eines Kapitels.

## chapterComplete

Signalisiert den Abschluss eines Kapitels.

## error

Signalisiert, dass ein Fehler aufgetreten ist.

## sessionEnd

Dieser Parameter wird verwendet, um das Media Analytics-Backend aufzufordern, die Sitzung umgehend zu schließen, wenn der Benutzer die Wiedergabe verlassen hat und wahrscheinlich nicht zurückkehren wird.

Wenn kein `sessionEnd` gesendet wird, wird eine abgebrochene Sitzung [Timeout normal](../mc-api-impl/mc-api-timeout.md) (entweder nachdem für 10 Minuten keine Ereignisse empfangen wurden oder wenn für 30 Minuten keine Abspielkopfbewegung stattfindet). Darüber hinaus werden alle nachfolgenden Medienaufrufe, die mit dieser Sitzungs-ID getätigt werden, entfernt.

## sessionComplete

Wird gesendet, wenn das Ende des Hauptinhalts erreicht ist.

>[!IMPORTANT]
>
>In den [JSON-Validierungsschemas](mc-api-json-validation.md) für die jeweiligen Ereignistypen finden Sie Informationen zur Überprüfung der Parametertypen und -anforderungen.

## stateStart

Signalisiert den Beginn der Player-Status-Verfolgung.

Weitere Informationen finden Sie unter [Implementierung und Reporting](/help/use-cases/player-state-tracking/implementation-and-reporting.md).

## stateEnd

Signalisiert das Ende der Statusverfolgung des Players.

Weitere Informationen finden Sie unter [Implementierung und Reporting](/help/use-cases/player-state-tracking/implementation-and-reporting.md).
