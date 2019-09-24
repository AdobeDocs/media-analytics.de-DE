---
seo-title: Senden von Ping-Ereignissen
title: Senden von Ping-Ereignissen
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Senden von Ping-Ereignissen{#sending-ping-events}

**Beim Hauptinhalt müssen Sie alle zehn Sekunden Ping-Ereignisse auslösen, die unabhängig von anderen gesendeten API-Aufrufen zehn Sekunden nach dem Start der Wiedergabe beginnen müssen. Zur Anzeigenverfolgung müssen Sie Ping-Ereignisse alle 1 Sekunde auslösen.**

Die Ping-Ereignisse sind wörtlich der "Heartbeat"von Media Analytics. Die einzigen für einen Ping-Aufruf erforderlichen Parameter sind `eventType: ping` sowie das Objekt `playerTime` (Abspielposition und Zeitstempel).

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

