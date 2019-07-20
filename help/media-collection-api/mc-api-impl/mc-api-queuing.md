---
seo-title: Einreihen von Ereignissen in die Warteschlange bei langsamer Sitzungsantwort
title: Einreihen von Ereignissen in die Warteschlange bei langsamer Sitzungsantwort
uuid: 39 ea 59 d 9-89 d 3-4087-a 806-48 a 43 ecf 0 c 98
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Einreihen von Ereignissen in die Warteschlange bei langsamer Sitzungsantwort{#queueing-events-when-sessions-response-is-slow}

Bei der Mediensammlungs-API handelt es sich um eine RESTful-API. Das heißt, Sie stellen eine HTTP-Anfrage und warten auf die Antwort. This is an important point only for when you make a [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) to obtain a Session ID at the beginning of video playback. Dies ist wichtig, da die Sitzungs-ID für alle nachfolgenden Verfolgungsaufrufe erforderlich ist.

It is possible that your player may fire events _before the Sessions response returns_ (with the Session ID parameter) from the backend. If this occurs, your app must queue any tracking events that arrive between the [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) and its response. When the Sessions response arrives, you should first process any queued [events](../../media-collection-api/mc-api-ref/mc-api-events-req.md), then you can start processing _live_ events with the [Events](../../media-collection-api/mc-api-ref/mc-api-events-req.md) calls.

>[!NOTE]
>
>Die [Ereignisanfrage](../../media-collection-api/mc-api-ref/mc-api-events-req.md) gibt neben einem HTTP-Antwortcode keine Daten an den Client zurück.

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
