---
title: Einreihen von Ereignissen in die Warteschlange bei langsamer Sitzungsantwort
description: 'Erfahren Sie, was zu tun ist, wenn die Sitzungs-ID zurückgegeben wird, nachdem Ihr Player Ereignisse auslöst. '
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 92%

---

# Einreihen von Ereignissen in die Warteschlange bei langsamer Sitzungsantwort{#queueing-events-when-sessions-response-is-slow}

Bei der Mediensammlungs-API handelt es sich um eine RESTful-API. Das heißt, Sie stellen eine HTTP-Anfrage und warten auf die Antwort. Das ist nur wichtig, wenn Sie zu Beginn der Videowiedergabe eine [Sitzungsanforderung](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) stellen, um eine Sitzungs-ID abzurufen. Dies ist wichtig, da die Sitzungs-ID für alle nachfolgenden Tracking-Anrufe erforderlich ist.

Der Player löst möglicherweise Ereignisse aus, _bevor Sitzungsantwort_ (mit dem Sitzungs-ID-Parameter) vom Backend zurückgegeben wird. In diesem Fall muss Ihre Anwendung sämtliche Tracking-Ereignisse in die Warteschlange einreihen, die zwischen der [Sitzungsanforderung](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) und ihrer Antwort eingehen. Wenn die Sitzungsantwort eingeht, sollten Sie zunächst alle [Ereignisse](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) in der Warteschlange verarbeiten. Anschließend können Sie mit den [Ereignisaufrufen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) mit der Verarbeitung von _Live_-Ereignissen beginnen.

>[!NOTE]
>
>Die [Ereignisanfrage](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) gibt neben einem HTTP-Antwortcode keine Daten an den Client zurück.

Im Referenz-Player in Ihrer Verteilung finden Sie eine Möglichkeit, Ereignisse vor dem Empfang der Sitzungs-ID zu verarbeiten. Beispiel:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**Sämtliche Ereignisse in der Warteschlange verarbeiten:** Der Referenz-Player verarbeitet die Ereignisse in der Warteschlange wie folgt:

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

Fahren Sie mit der Verarbeitung laufender Tracking-Ereignisse fort.
