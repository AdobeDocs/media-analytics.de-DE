---
title: 'Test 2: Medienunterbrechung'
description: Erfahren Sie mehr über den Medienunterbrechungstest, der bei der Validierung verwendet wird.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 96%

---

# Test 2: Medienunterbrechung {#test-media-interruption}

In diesem Testfall wird das Verhalten von Mobilgeräten bei Unterbrechungen überprüft.

## Testverfahren

Sie müssen diese Aufgaben in folgender Reihenfolge abschließen und aufzeichnen:

1. **Medienplayer starten**

   Wenn der Medienplayer gestartet wird, werden die Aufrufe in folgender Reihenfolge gesendet:

   1. Start für Adobe Analytics (AppMeasurement)
   1. Start für Media Analytics (Heartbeats)
   1. Start-Aufruf für Adobe Analytics in Media Analytics (Heartbeats) angefordert

   Die ersten beiden Aufrufe oben enthalten zusätzliche Metadaten und Variablen. Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Der dritte Aufruf oben teilt dem Media Analytics-Server mit, dass das Media SDK angefordert hat, den Start-Aufruf für Adobe Analytics (`pev2=ms_s`) an den Adobe Analytics-Server zu senden.

1. **Hauptinhalt mindestens fünf Minuten lang unterbrechungsfrei wiedergeben**

   **Content Play**

   Während der Wiedergabe des Inhalts sendet das Media SDK alle 10 Sekunden Abspielaufrufe (Heartbeats) an den Media Analytics-Server.

   Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zum Testaufruf.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Weitere Informationen zu diesen Anzeigenaufrufen finden Sie in den Anleitungen zum [Tracking von Anzeigen](/help/sdk-implement/track-ads/track-ads-overview.md) Ihrer Plattform.

1. **App oder Browser im Hintergrund ausführen**

   Während die App im Hintergrund ausgeführt wird, sollten ab VHL-Version 1.6.6 nur `main:pause`-Aufrufe an den Media Analytics-Server gesendet werden.

1. **App oder Browser erneut anzeigen**

   Wenn die App nach der Ausführung im Hintergrund erneut angezeigt wird, sollte die Inhaltswiedergabe fortgesetzt werden.

1. **Hauptinhaltsmedium mindestens fünf Minuten lang unterbrechungsfrei wiedergeben**

   Informationen zu Aufrufparametern und Metadaten finden Sie unter [Details zu Testaufrufen.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Medienplayer schließen**

   Nachdem der Medienplayer geschlossen wurde, sollten keine zusätzlichen Tracking-Aufrufe mehr ausgelöst werden.
