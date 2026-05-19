---
title: Behandlung von Anwendungsunterbrechungen während der Wiedergabe
description: Erfahren Sie, wie Sie Unterbrechungen beim Tracking während der Medienwiedergabe behandeln können.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/BlL-c1rf5d3juDKHybex9vrPvQsBIiNXVO2ug9LKl0g
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 41%

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

  Informationen zum Wiederaufnehmen einer Tracking-Sitzung finden Sie unter [Wiederaufnehmen von inaktiven Sitzungen](resuming-inactive.md).SDK sendet ein Wiederaufnahme-Ping, um das Backend darüber zu informieren, dass die Sitzung manuell wieder aufgenommen wird.

* _Was passiert, wenn `trackSessionEnd` für dieselbe Sitzung zweimal aufgerufen wird?_

  `trackSessionEnd` mehrmals für dieselbe Sitzung aufzurufen ist sicher. Das Backend schließt die Sitzung beim ersten Ereignis und löscht alle nachfolgenden Ereignisse für diese Sitzungs-ID, einschließlich eines zweiten `trackSessionEnd`, im Hintergrund. Dies bedeutet, dass die Race-Bedingungen - z. B. die 30-minütige Inaktivitäts-Zeitüberschreitung, die in dem Moment ausgelöst wird, in dem der Viewer den Player schließt - keine doppelten Daten erzeugen.

* _Was passiert, wenn `trackSessionStart` aufgerufen wird, während eine Sitzung bereits aktiv ist?_

  SDK ignoriert den zweiten `trackSessionStart`, wenn die Sitzung noch nicht geschlossen wurde. Wenn Sie eine neue Sitzung starten müssen, rufen Sie zuerst `trackSessionEnd` auf, um die aktuelle Sitzung explizit zu schließen, und rufen Sie dann `trackSessionStart` für die neue Sitzung auf.
