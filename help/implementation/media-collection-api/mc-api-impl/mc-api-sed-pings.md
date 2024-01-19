---
title: Senden von Ping-Ereignissen
description: Ping-Ereignisse sind der Herzschlag von Streaming Media Analytics. Erfahren Sie, wie Sie einen zeitgesteuerten Ping für Haupt- oder Anzeigen-Tracking senden.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e84864164adf056f47f24d65f0400c89d53d1630
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 70%

---

# Senden von Ping-Ereignissen{#sending-ping-events}

**Sie müssen alle zehn Sekunden Ping-Ereignisse auslösen, die unabhängig von anderen gesendeten API-Ereignissen nach 10 Sekunden der Wiedergabe beginnen. Dies gilt sowohl für den Hauptinhalt als auch für das Anzeigen-Tracking.**

Die Ping-Ereignisse sind buchstäblich der „Herzschlag“ von Media Analytics. Die einzigen für einen Ping-Aufruf erforderlichen Parameter sind `eventType: ping` sowie das Objekt `playerTime` (Abspielposition und Zeitstempel).

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
