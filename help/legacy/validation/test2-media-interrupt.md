---
title: 'Test 2: Medienunterbrechung'
description: Erfahren Sie mehr über den Medienunterbrechungstest, der bei der Validierung verwendet wird.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# Test 2: Medienunterbrechung{#test-media-interruption}

In diesem Testfall wird das Verhalten von Mobilgeräten bei Unterbrechungen überprüft.

## Testverfahren

Sie müssen diese Aufgaben in folgender Reihenfolge abschließen und aufzeichnen:

1. **Medienplayer starten**

   Wenn der Medienplayer gestartet wird, werden die Aufrufe in folgender Reihenfolge gesendet:

   1. Start für Adobe Analytics (AppMeasurement)
   1. Start für Media Analytics (Heartbeats)
   1. Start-Aufruf für Adobe Analytics in Media Analytics (Heartbeats) angefordert

   Die ersten beiden Aufrufe oben enthalten zusätzliche Metadaten und Variablen. Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   Der dritte Aufruf oben teilt dem Media Analytics-Server mit, dass das Media SDK angefordert hat, den Start-Aufruf für Adobe Analytics (`pev2=ms_s`) an den Adobe Analytics-Server zu senden.

1. **Hauptinhalt mindestens fünf Minuten lang unterbrechungsfrei wiedergeben**

   **Content Play**

   Während der Wiedergabe des Inhalts sendet das Media SDK alle 10 Sekunden Abspielaufrufe (Heartbeats) an den Media Analytics-Server.

   Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf.](/help/legacy/validation/test-call-details.md#play-main-content)

   Weitere Informationen zu diesen Anzeigenaufrufen finden Sie in den Anleitungen zum [Nachverfolgen von Anzeigen](/help/use-cases/track-ads/track-ads-overview.md) Ihrer Plattform.

1. **App oder Browser im Hintergrund ausführen**

   Während die App im Hintergrund ausgeführt wird, sollten ab VHL-Version 1.6.6 nur `main:pause`-Aufrufe an den Media Analytics-Server gesendet werden.

1. **App oder Browser erneut anzeigen**

   Wenn die App nach der Ausführung im Hintergrund erneut angezeigt wird, sollte die Inhaltswiedergabe fortgesetzt werden.

1. **Hauptinhaltsmedium mindestens fünf Minuten lang unterbrechungsfrei wiedergeben**

   Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zu Testaufrufen.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Medienplayer schließen**

   Nachdem der Medienplayer geschlossen wurde, sollten keine zusätzlichen Tracking-Aufrufe mehr ausgelöst werden.
