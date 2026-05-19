---
title: Steuern der Ereignisreihenfolge
description: Erfahren Sie, wie Sie die Reihenfolge der Ereignisse steuern und wie in einigen Fällen Ereignisse basierend auf dem bereitgestellten Zeitstempel im playerTime-Objekt neu angeordnet werden.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 342
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
