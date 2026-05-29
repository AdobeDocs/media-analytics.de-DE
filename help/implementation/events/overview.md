---
title: Übersicht über Streaming-Medienereignisse
description: Erfahren Sie mehr über Medienereignistypen und die Reihenfolge, in der sie gesendet werden müssen.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---


# Streaming-Medienereignisse

Beim Tracking von Streaming-Medien wird eine Sequenz von Ereignisaufrufen an einen Datenerfassungsendpunkt von Adobe gesendet, die jeweils eine Transition im Status des Players darstellen. Jedes Ereignis gehört zu einer aktiven Sitzung, die durch einen [Sitzungsstart](session/session-start.md)-Aufruf geöffnet wird. Sitzungen werden automatisch durch Ablauf geschlossen oder können sofort mit einem Aufruf [Sitzungsende](session/session-end.md) geschlossen werden.

Ereignisse werden in sechs Kategorien gruppiert (Sitzung, Wiedergabe, Anzeigen, Kapitel, Player-Status und Qualität), wobei jede einen bestimmten Aspekt des Medienerlebnisses abdeckt.

## Sitzungsereignisse

Sitzungsereignisse gelten für jede Art von Medien-Tracking, einschließlich Video-on-Demand, Live-Streams, Podcasts und Hörbüchern. Sie definieren die Grenzen der Tracking-Sitzung selbst. Das wichtigste Sitzungsereignis ist [Sitzungsstart](session/session-start.md) da fast jeder andere Ereignistyp von der generierten Sitzungs-ID abhängt. Senden Sie es als erstes Ereignis, wenn ein Benutzer eine Sitzung einleitet, z. B. wenn er die Wiedergabetaste drückt oder wenn der Player mit der automatischen Wiedergabe beginnt.

Sobald eine Sitzung geöffnet ist, verwenden Sie [Sitzung abgeschlossen](session/session-complete.md) oder [Sitzungsende](session/session-end.md) um anzugeben, wie das Anzeigeerlebnis beendet wurde. Die Sendesitzung ist abgeschlossen, wenn der Betrachter das natürliche Ende des Inhalts erreicht - das Video ist beendet, die Podcast-Folge endet oder das letzte Kapitel eines Hörbuchs endet. Sitzung abgeschlossen schließt die Sitzung nicht. Sie bleibt offen, bis sie automatisch abläuft, sodass alle nachfolgenden Ereignisse, wie z. B. ein endgültiges Ping, weiterhin erfasst werden.

Wenn der Betrachter die Sitzung verlässt, bevor er das Ende erreicht[ senden Sie „Sitzungsende](session/session-end.md), um die Sitzung sofort zu schließen. Senden Sie die Sitzung nur, wenn keine weiteren Ereignisse folgen, z. B. wenn der Player zerstört oder die Seite entladen wurde. Das Ende der Sitzung ist ein harter Abschluss: Nach dem Versand wird die Sitzung beendet und es können keine weiteren Ereignisse darunter verfolgt werden. In den meisten Fällen ist es sicherer, die Sitzung auf natürliche Weise ablaufen zu lassen. Beispiele sind das Pausieren des Viewers auf unbestimmte Zeit, das Wechseln der App in den Hintergrund oder das Nichtladen des Inhalts.

Eine Sitzung läuft automatisch ab, wenn für 10 Minuten keine Ereignisse empfangen werden oder wenn für 30 Minuten keine Abspielkopfbewegung erkannt wird. Wenn eine der Bedingungen erfüllt ist und der Viewer zum Inhalt zurückkehrt, müssen Sie Sitzungsstart erneut aufrufen, um eine neue Sitzung zu öffnen, bevor Sie weitere Ereignisse senden.

## Wiedergabeereignisse

Wiedergabeereignisse verfolgen Statusübergänge im Media Player während einer Sitzung. Sie bilden den Kern des Ereignis-Streams und gelten für jeden Inhaltstyp.

Das primäre Wiedergabeereignis ist [Play](playback/play.md). Nach dem Aufruf von Sitzungsstart gibt Play an, dass die Wiedergabe des Inhalts begonnen hat - ob es sich um den ersten Start, einen Trigger für die automatische Wiedergabe oder eine Rückkehr zum Wiedergabestatus handelt. [Start anhalten](playback/pause-start.md) gibt an, dass die Wiedergabe angehalten wurde. Es gibt kein dediziertes Wiederaufnahmeereignis. Senden Sie die Wiedergabe erneut, wenn der Viewer sie wiederaufnimmt. Die Wiedergabe funktioniert nach einem Pufferüberhang genauso: Senden Sie [Pufferstart](playback/buffer-start.md), wenn der Player auf Daten wartet, und folgen Sie dann mit Wiedergabe, wenn die Pufferung aufgelöst wird.

Senden Sie [Ping](playback/ping.md) alle 10 Sekunden während der Wiedergabe des Hauptinhalts und alle 1 Sekunde während der Anzeigenwiedergabe. Ping hält die Sitzung am Leben und zeichnet Abspielkopfbewegungen auf. Bei Mobile SDKs werden Pings automatisch gesendet. Bei allen anderen Plattformen müssen sie manuell gesendet werden.

Senden Sie [Bitratenänderung](playback/bitrate-change.md) immer dann, wenn der Algorithmus des Players für die adaptive Bitrate auf eine andere Qualitätsstufe wechselt. Die Einbeziehung des neuen Bitratenwerts in die QoE-Daten ermöglicht die Berichterstellung für die durchschnittliche Bitrate.

## Ereignisse hinzufügen

Anzeigen-Ereignisse verfolgen Werbung innerhalb einer Mediensitzung. Häufige Szenarien sind Pre-Roll-Anzeigen vor dem Beginn eines Videos, Mid-Roll-Anzeigen, die in Intervallen während eines langen Video- oder Live-Streams eingefügt werden, und Post-Roll-Anzeigen nach dem Ende des Inhalts. Eine einzelne Werbeunterbrechung kann eine oder mehrere einzelne Anzeigen enthalten.

Jede Werbeunterbrechung folgt derselben Struktur. [Start der Werbeunterbrechung](ads/ad-break-start.md) öffnet die Unterbrechung und [Werbeunterbrechung abgeschlossen](ads/ad-break-complete.md) schließt sie. Diese beiden Ereignisse fungieren als Buchstützen, die alle einzelnen Anzeigenereignisse einschließen. Senden Sie innerhalb der Pause [Anzeigenstart](ads/ad-start.md) , wenn jede einzelne Anzeige zu spielen beginnt. Hiermit klicken Sie auf [Anzeige abgeschlossen](ads/ad-complete.md) wenn die Anzeige auf ihre volle Länge wiedergegeben wird, oder [Anzeige überspringen](ads/ad-skip.md) wenn der Viewer auf die Schaltfläche Überspringen klickt. Das Auslassen eines der Buchenden führt dazu, dass alle Anzeigenereignisse in der Pause ignoriert werden und die Anzeigendauer fälschlicherweise dem Hauptinhalt zugeordnet wird.

Das folgende Beispiel zeigt die richtige Ereignissequenz für eine einzelne Werbeunterbrechung mit drei Anzeigen, bei der der Viewer die dritte übersprungen hat:

1. Start der Werbeunterbrechung
2. Anzeigenstart
3. Hinzufügen abgeschlossen
4. Anzeigenstart
5. Hinzufügen abgeschlossen
6. Anzeigenstart
7. Überspringen einer Anzeige
8. Werbeunterbrechung abgeschlossen

## Kapitelereignisse

Kapitelereignisse sind optional und verfolgen benannte Inhaltssegmente innerhalb einer Sitzung. Sie eignen sich gut für Inhalte, die auf natürliche Weise in separate Teile unterteilt werden. Häufige Beispiele sind Kapitel in einem Hörbuch, Acts in einer Dokumentation, Lektionen in einem Videokurs oder Segmente in einer Podcast-Folge. Verwenden Sie Kapitelereignisse, wenn Sie die Interaktion mit Betrachtern auf Segmentebene verstehen möchten, z. B. die Identifizierung von Kapiteln, die Zielgruppen überspringen.

Senden Sie [Kapitelstart](chapters/chapter-start.md) wenn ein Kapitel beginnt. Wenn der Betrachter bis zum Ende des Kapitels wacht, senden Sie [Chapter complete](chapters/chapter-complete.md). Wenn der Betrachter über die Kapitelgrenze hinaus sucht, ohne sie bis zum Ende anzusehen, senden Sie stattdessen [Kapitelüberspringen](chapters/chapter-skip.md). Ein Kapitel muss entweder mit „Kapitel abgeschlossen“ oder „Kapitel überspringen“ geschlossen werden, bevor ein neues geöffnet werden kann. Kapitel dürfen sich nicht überschneiden.

## Player-Statusereignisse

Player-Statusereignisse verfolgen, wie Viewer während einer Sitzung mit Player-Steuerelementen interagieren. Sie sind nützlich, um die Verwendung von Barrierefreiheitsfunktionen zu verstehen, z. B. wie oft Viewer Untertitel aktivieren oder stumm schalten. Sie zeigen auch das Betrachtungsverhalten von Mustern wie Vollbildmodus im Vergleich zu Inline-Anzeige und Bild-in-Bild-Multitasking.

Die fünf nachverfolgbaren Status sind: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` und `inFocus`. Senden Sie [Status starten](player-state/state-start.md) wenn der Player in einen dieser Status wechselt, und [Status endet](player-state/state-end.md) wenn er beendet wird. Es können mehrere Status gleichzeitig aktiv sein. Ein Viewer kann im Vollbildmodus angezeigt und gleichzeitig stummgeschaltet werden, und es können mehrere Status innerhalb desselben Ereignisaufrufs beendet werden.

## Fehlerereignisse

Das [Fehler](error.md)-Ereignis zeichnet einen Wiedergabefehler während einer Sitzung auf - eine fehlgeschlagene Stream-Anfrage, einen Codec-Fehler oder einen externen Versandfehler. Senden Sie ihn, wenn ein bedeutender Fehler auftritt. Ein Fehlerereignis schließt die Sitzung nicht. Die Wiedergabe kann fortgesetzt werden, und nachfolgende Ereignisse werden in derselben Sitzung verfolgt. Wenn der Fehler nicht behebbar ist, folgen Sie ihm mit Sitzungsende , um die Sitzung explizit zu schließen.
