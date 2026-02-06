---
title: Behandlung von Anwendungsunterbrechungen während der Wiedergabe
description: Erfahren Sie, wie Sie Unterbrechungen beim Tracking während der Medienwiedergabe behandeln können.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 63%

---

# Behandlung von Anwendungsunterbrechungen während der Wiedergabe{#handling-application-interrupts-during-playback}

Die Wiedergabe in einer Medienanwendung kann auf verschiedene Weise unterbrochen werden. Beispielsweise kann explizit die Pause-Taste betätiget oder die Anwendung in den Hintergrund gebracht werden. Unabhängig davon, was zu einer Unterbrechung der Medienwiedergabe führt, gelten die folgenden Tracking-Anweisungen.

1. Rufen Sie **`trackPause`** auf, wenn die Anwendung unterbrochen wird (Hintergrund, Medienpausen usw.).
1. Rufen Sie **`trackPlay`** auf, wenn die Anwendung in den Vordergrund zurückkehrt und/oder die Medienwiedergabe fortgesetzt wird.

>[!NOTE]
>
>Der Aufruf von `trackSessionStart`, wenn die App vom Hintergrund zurückkehrt, kann dazu führen, dass die Wiedergabe bis zu diesem Zeitpunkt nicht für die gesamte Wiedergabezeit zählt, zusammen mit dem Verlust früherer Fortschrittsmarken, Segmente usw. Rufen Sie stattdessen `trackPlay` auf, wenn die App wieder geöffnet oder die Medienwiedergabe fortgesetzt wird.

## Häufige Fragen zur Behandlung von Anwendungsunterbrechungen: {#faq-about-handling-application-interrupts}

* _Wie lange sollte eine App im Hintergrund sein, bevor die Sitzung geschlossen wird?_

  Wenn die Anwendung die Hintergrundwiedergabe zulässt, kann sie das Tracking fortsetzen, indem sie unsere APIs aufruft, und wir senden alle unsere regelmäßigen Tracking-Pings. Nur wenige Video-Apps erlauben die Wiedergabe im Hintergrund, außer YouTube Red. Dies ist jedoch in allen Audio-Apps möglich. Wenn die Anwendung keine Hintergrundwiedergabe zulässt, ist es ratsam, eine Minute lang im Pausenstatus zu bleiben und dann die Tracking-Sitzung zu beenden. Die Anwendung kann keine Pausen-Pings mehr senden, da in den meisten Fällen nicht festgestellt werden kann, ob der Benutzer zurückkehrt, um die Anzeige des Mediums fortzusetzen, oder wann es beendet wird. Es ist auch eine schlechte Erfahrung, im Hintergrund weiterhin Pings zu senden.

* _Wie kann das Tracking beim Neustart korrekt gehandhabt werden, nachdem die App lange Zeit im Hintergrund war?_

  Die Anwendung sollte `trackSessionEnd` aufrufen, um die Tracking-Sitzung zu beenden. Ab Version 2.1 sendet der SDK einen „End“-Ping, um das Backend darüber zu informieren, dass die Tracking-Sitzung geschlossen ist.

* _Wie wäre es, dieselbe Sitzung neu zu starten?_

  Informationen zum Wiederaufnehmen einer Tracking-Sitzung finden Sie unter [Wiederaufnehmen von inaktiven Sitzungen](resuming-inactive.md)..Das SDK sendet ein Wiederaufnahme-Ping, um das Backend darüber zu informieren, dass die Sitzung manuell wiederaufgenommen wird.
