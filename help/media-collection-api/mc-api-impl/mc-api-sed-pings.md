---
title: Senden von Ping-Ereignissen
description: Senden von Ping-Ereignissen
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '88'
ht-degree: 100%

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
