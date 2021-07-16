---
title: Senden von Ping-Ereignissen
description: Ping-Ereignisse sind der Herzschlag von Streaming Media Analytics. Erfahren Sie, wie Sie einen zeitgesteuerten Ping für Haupt- oder Anzeigen-Tracking senden.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 100%

---

# Senden von Ping-Ereignissen{#sending-ping-events}

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
