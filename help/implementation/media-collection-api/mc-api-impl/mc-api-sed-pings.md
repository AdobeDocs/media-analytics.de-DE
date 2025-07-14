---
title: Senden von Ping-Ereignissen
description: Ping-Ereignisse sind der Herzschlag der Streaming-Mediensammlung. Erfahren Sie, wie Sie einen zeitgesteuerten Ping für Haupt- oder Anzeigen-Tracking senden.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 51%

---

# Senden von Ping-Ereignissen{#sending-ping-events}

**Sie müssen unabhängig von anderen von Ihnen gesendeten API-Ereignissen alle 10 Sekunden ab 10 Sekunden der Wiedergabe Ping-Ereignisse auslösen. Dies gilt sowohl für das Haupt-Content- als auch für das Anzeigen-Tracking.**

Die Ping-Ereignisse sind der „Heartbeat“ der Streaming-Mediensammlung. Die einzigen für einen Ping-Aufruf erforderlichen Parameter sind `eventType: ping` sowie das Objekt `playerTime` (Abspielposition und Zeitstempel).

Der folgende Codeausschnitt zeigt eine Möglichkeit, einen zeitgesteuerten Ping-Mechanismus für Hauptinhalte zu implementieren (10-Sekunden-Intervall):

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
