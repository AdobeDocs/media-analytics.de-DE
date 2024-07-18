---
title: Senden von Ping-Ereignissen
description: Ping-Ereignisse sind der Herzschlag des Streaming-Mediensammlungs-Add-ons. Erfahren Sie, wie Sie einen zeitgesteuerten Ping für Haupt- oder Anzeigen-Tracking senden.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 50%

---

# Senden von Ping-Ereignissen{#sending-ping-events}

**Sie müssen alle 10 Sekunden Ping-Ereignisse auslösen, die unabhängig von anderen gesendeten API-Ereignissen nach 10 Sekunden der Wiedergabe beginnen. Dies gilt sowohl für den Hauptinhalt als auch für das Anzeigen-Tracking.**

Die Ping-Ereignisse sind der &quot;Heartbeat&quot;des Add-ons für Streaming-Mediensammlung. Die einzigen für einen Ping-Aufruf erforderlichen Parameter sind `eventType: ping` sowie das Objekt `playerTime` (Abspielposition und Zeitstempel).

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
