---
seo-title: Einstellen des HTTP-Anfragetyps in Ihrem Player
title: Einstellen des HTTP-Anfragetyps in Ihrem Player
uuid: b 8 fa 7233-e 654-4 acf-a 9 d 7-14158 cded 13 e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Setting the HTTP request type {#setting-the-http-request-type}

Der Anfrageinhalt für alle Mediensammlungs-API-Anfragen muss im JSON-Format vorliegen. Dementsprechend sollten Sie den Inhaltsanfragetyp in Ihrem Player festlegen. In JavaScript würden Sie beispielsweise den Anfrage-Header `Content-Type` wie folgt festlegen:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

