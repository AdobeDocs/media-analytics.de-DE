---
seo-title: Senden von Ping-Ereignissen
title: Senden von Ping-Ereignissen
uuid: c 92 c 1 a 92-3 af 6-4474-9 e 42-ffb 8 f 6 c 94 b 33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Senden von Ping-Ereignissen{#sending-ping-events}

**Beim Hauptinhalt müssen Sie alle zehn Sekunden Ping-Ereignisse auslösen, die unabhängig von anderen gesendeten API-Aufrufen zehn Sekunden nach dem Start der Wiedergabe beginnen müssen. For Ad tracking, you must fire ping events every 1 second.**

Die Ping-Ereignisse sind wortwörtlich der "Heartbeat" von Media Analytics. Die einzigen für einen Ping-Aufruf erforderlichen Parameter sind `eventType: ping` sowie das Objekt `playerTime` (Abspielposition und Zeitstempel).

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

