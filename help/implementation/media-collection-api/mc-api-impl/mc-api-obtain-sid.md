---
title: Beziehen einer Sitzungs-ID
description: Erfahren Sie, wie Sie eine Sitzungsanfrage codieren, um die Sitzungs-ID aus dem Location-Header in einer Antwort zu erhalten.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 100%

---

# Beziehen einer Sitzungs-ID {#obtaining-a-session-id}

Dieser Code-Ausschnitt aus dem Referenz-Player zeigt eine Möglichkeit, eine [Sitzungsanfrage](../mc-api-ref/mc-api-sessions-req.md) zu codieren und die Sitzungs-ID (und die Version der Mediensammlungs-API) aus der Speicherort-Kopfzeile der Antwort zu extrahieren:

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```
