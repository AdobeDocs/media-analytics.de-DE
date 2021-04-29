---
title: Steuern der Ereignisreihenfolge
description: Steuern der Ereignisreihenfolge
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: 27694ec83de89980404df7a7cc77fa42b3d1a751
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%

---

# Steuern der Ereignisreihenfolge {#controlling-the-order-of-events}

Die Streaming-Videoverfolgung ist in hohem Maße zeitabhängig, und gelegentlich werden die Media Collection-API-Verfolgungsaufrufe im Back-End nicht ordnungsgemäß gesendet. In diesem Fall versucht das Back-End, Ereignis basierend auf dem bereitgestellten Zeitstempel im `playerTime`-Objekt in eine Warteschlange zu stellen und neu anzuordnen.  Dies geschieht mit einigen Einschränkungen. Derzeit kann die Neuanordnung fehlschlagen, wenn die Verzögerungen zwischen nicht sortierten Aufrufen mehr als eine Sekunde betragen. In zukünftigen Updates kann die &quot;akzeptable Zeitverzögerung&quot;optimiert und konfiguriert werden.

## Beispiel für ein nicht in der Reihenfolge befindliches Ereignis

Ereignis, die nicht in der richtigen Reihenfolge auftreten, treten auf, wenn Ereignis das Netzwerk passieren, was manchmal zu einer Verzögerung führt.

Sie können beispielsweise ein `adBreakStart`-Ereignis gefolgt von einem `adStart`-Ereignis senden. Dies ist ein gängiger Anwendungsfall, da er für eine Anzeige zum Beginn innerhalb einer Werbeunterbrechung erforderlich ist.

Wenn die Anzeige fertig ist und kein Puffer erforderlich ist, treten beide Ereignis fast sofort auf und die `playerTime.ts` für beide Ereignis sind sehr nahe beieinander - sie sollten jedoch nie gleich sein.

> &quot;playerTime.ts&quot;von Ereignissen sollte für kein Ereignis gleich sein, da der Sortieralgorithmus nicht wusste, was zuerst passiert ist. Es sollte mindestens eine Millisekunde Zeitstempeldifferenz für alle zwei aufeinander folgenden Ereignis geben.

Da sich beide Ereignis beim Auslösen von Netzwerkaufrufen sehr nahe beieinander befinden, ist es möglich, dass sie nicht in der richtigen Reihenfolge ankommen. In diesem Beispiel wird das Ereignis `adStart` vor dem Ereignis `adBreakStart` angekommen.


Es gibt ein Zeitfenster mit Ereignissen: 5 Sekunden oder maximal 10 Ereignis. Die Ereignis werden gepuffert, bevor sie an die Verarbeitungspipeline gesendet werden. Wenn die Bedingungen erfüllt sind - 5 Sekunden vergangen sind oder mehr als 10 Ereignis empfangen werden, werden die Ereignis basierend auf dem `playerTime.ts` neu angeordnet und dann in der neuen Reihenfolge an die Verarbeitungspipeline gesendet.

>[!IMPORTANT]
>
>Es gibt ein Ausnahmefehler-Ereignis, das sofort an die Verarbeitungspipeline gesendet wird, und zwar das Ereignis `sessionStart`.
