---
title: Senden von Ping-Ereignissen
description: null
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Senden von Ping-Ereignissen {#sending-ping-events}

**Beim Hauptinhalt müssen Sie alle zehn Sekunden Ping-Ereignisse auslösen, die unabhängig von anderen gesendeten API-Aufrufen zehn Sekunden nach dem Start der Wiedergabe beginnen müssen. Für das Anzeigen-Tracking müssen Sie jede Sekunden Ping-Ereignisse auslösen.**

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

