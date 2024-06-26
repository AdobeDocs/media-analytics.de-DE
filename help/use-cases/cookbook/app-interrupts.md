---
title: Behandlung von Anwendungsunterbrechungen während der Wiedergabe
description: Erfahren Sie, wie Sie Unterbrechungen beim Tracking während der Medienwiedergabe behandeln können.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 90%

---

# Behandlung von Anwendungsunterbrechungen während der Wiedergabe{#handling-application-interrupts-during-playback}

Die Wiedergabe in einer Medienanwendung kann auf verschiedene Weise unterbrochen werden. Beispielsweise kann explizit die Pause-Taste betätiget oder die Anwendung in den Hintergrund gebracht werden. Unabhängig davon, was zu einer Unterbrechung der Medienwiedergabe führt, gelten die folgenden Tracking-Anweisungen.

1. Rufen Sie **`trackPause`** auf, wenn die Anwendung unterbrochen wird (Hintergrund, Medienpausen usw.).
1. Rufen Sie **`trackPlay`** auf, wenn die Anwendung in den Vordergrund zurückkehrt und/oder die Medienwiedergabe fortgesetzt wird.

>[!NOTE]
>
>Aufruf `trackSessionStart` Wenn die App aus dem Hintergrund zurückkehrt, kann dies dazu führen, dass die Wiedergabe bis zu diesem Zeitpunkt nicht auf die gesamte Wiedergabedauer angerechnet wird und frühere Fortschrittsmarken, Segmente usw. verloren gehen. Rufen Sie stattdessen `trackPlay` auf, wenn die App wieder geöffnet oder die Medienwiedergabe fortgesetzt wird.

## Häufige Fragen zur Behandlung von Anwendungsunterbrechungen: {#faq-about-handling-application-interrupts}

* _Wie lange sollte eine App im Hintergrund laufen, bevor die Sitzung beendet wird?_

  Wenn die Anwendung die Hintergrundwiedergabe erlaubt, kann das Tracking mit dem Aufruf unserer APIs fortgesetzt werden. Wir werden dann alle unsere regulären Verfolgungspings senden. Nur wenige Video-Apps erlauben die Wiedergabe im Hintergrund, außer YouTube Red. Dies ist jedoch in allen Audio-Apps möglich. Wenn die Anwendung keine Hintergrundwiedergabe zulässt, ist es ratsam, eine Minute lang im Pausenstatus zu bleiben und dann die Tracking-Sitzung zu beenden. Die Anwendung kann keine Pausen-Pings mehr senden, da in den meisten Fällen nicht festgestellt werden kann, ob der Benutzer zurückkehrt, um die Anzeige des Mediums fortzusetzen, oder wann es beendet wird. Es ist auch ein schlechtes Erlebnis, wenn Pings im Hintergrund versendet werden.

* _Welches ist der richtige Weg für einen Tracking-Neustart, wenn die App längere Zeit im Hintergrund war?_

  Die Anwendung sollte `trackSessionEnd` aufrufen, um die Tracking-Sitzung zu beenden. Ab Version 2.1 sendet das SDK ein „Ende“-Ping, um das Backend darüber zu informieren, dass die Tracking-Sitzung geschlossen wurde.

* _Wie sieht es mit einem Neustart der gleichen Sitzung aus?_

  Informationen zum Wiederaufnehmen einer Tracking-Sitzung finden Sie unter [Wiederaufnehmen von inaktiven Sitzungen](resuming-inactive.md)..Das SDK sendet ein Wiederaufnahme-Ping, um das Backend darüber zu informieren, dass die Sitzung manuell wiederaufgenommen wird.
