---
title: Einstellen des HTTP-Anfragetyps in Ihrem Player
description: 'Der Anfrageinhalt für alle Streaming Media Collection API-Anfragen muss im JSON-Format vorliegen. Erfahren Sie, wie Sie den Content-Anfragetyp in Ihrem Player festlegen. '
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Einstellen des HTTP-Anforderungstyps {#setting-the-http-request-type}

Der Anfrageinhalt für alle Mediensammlungs-API-Anfragen muss im JSON-Format vorliegen. Dementsprechend sollten Sie den Inhaltsanfragetyp in Ihrem Player festlegen. In JavaScript würden Sie beispielsweise den Anfrage-Header `Content-Type` wie folgt festlegen:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
