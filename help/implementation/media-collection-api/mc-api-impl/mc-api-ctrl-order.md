---
title: Steuern der Ereignisreihenfolge
description: Erfahren Sie, wie Sie die Reihenfolge der Ereignisse steuern und wie in einigen Fällen Ereignisse basierend auf dem bereitgestellten Zeitstempel im playerTime-Objekt neu angeordnet werden.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%

---

# Steuern der Ereignisreihenfolge{#controlling-the-order-of-events}

Die Verfolgung von Streaming-Videos ist in hohem Maße zeitabhängig, und gelegentlich werden die Media Collection-API-Verfolgungsaufrufe im Back-End nicht ordnungsgemäß gesendet. Das Back-End versucht in solchen Fällen, die Ereignisse in eine Warteschlange einzureihen und je nach Zeitstempel im Objekt `playerTime` neu zu ordnen.  Dies geschieht mit einigen Einschränkungen. Aktuell kann die Neusortierung fehlschlagen, wenn die Verzögerung zwischen den nicht ordnungsgemäß eingehenden Aufrufen mehr als eine Sekunde beträgt. In zukünftigen Updates wird es eventuell möglich sein, die „akzeptable Zeitverzögerung“ zu optimieren und zu konfigurieren.

## Beispiel für ein nicht in der Reihenfolge befindliches Ereignis

Ereignisse, die nicht in der richtigen Reihenfolge auftreten, werden ausgelöst, wenn Ereignisse das Netzwerk passieren, was manchmal zu einer Verzögerung führt.

Sie könnten beispielsweise ein `adBreakStart`-Ereignis gefolgt von einem `adStart`-Ereignis senden. Dies ist ein gängiger Anwendungsfall, da es für den Start einer Anzeige innerhalb einer Werbeunterbrechung erforderlich ist.

Wenn die Anzeige bereit und kein Puffer erforderlich ist, finden beide Ereignis praktisch sofort statt und die `playerTime.ts` für beide Ereignis liegen sehr nahe beieinander – sie sollten jedoch nie gleich sein.

> Der Ereigniswert „playerTime.ts“ sollte für kein Ereignis gleich sein, da der Sortieralgorithmus sonst nicht feststellen kann, welches Ereignis zuerst eintrat. Bei allen aufeinander folgenden Ereignissen sollten die Zeitstempel mindestens eine Millisekunde auseinander liegen.

Da sich beide Ereignisse beim Auslösen von Netzwerkaufrufen sehr nahe beieinander befinden, ist es möglich, dass sie nicht in der richtigen Reihenfolge ankommen. In diesem Beispiel kommt das Ereignis `adStart` vor dem Ereignis `adBreakStart` an.


Es gibt ein Zeitfenster für Ereignisse: 5 Sekunden oder maximal 10 Ereignisse. Die Ereignisse werden gepuffert, bevor sie an die Verarbeitungs-Pipeline gesendet werden. Wenn die Bedingungen erfüllt sind – wenn also 5 Sekunden vergangen oder mehr als 10 Ereignisse empfangen werden –, werden die Ereignisse basierend auf dem Wert `playerTime.ts` neu angeordnet und dann in der neuen Reihenfolge an die Verarbeitungs-Pipeline gesendet.

>[!IMPORTANT]
>
>Das Ereignis `sessionStart` stellt eine Ausnahme dar und wird sofort an die Verarbeitungs-Pipeline gesendet.
