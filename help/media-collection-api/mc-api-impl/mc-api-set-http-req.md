---
title: Einstellen des HTTP-Anfragetyps in Ihrem Player
description: Einstellen des HTTP-Anfragetyps in Ihrem Player
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '58'
ht-degree: 100%

---

# Einstellen des HTTP-Anforderungstyps {#setting-the-http-request-type}

Der Anfrageinhalt für alle Mediensammlungs-API-Anfragen muss im JSON-Format vorliegen. Dementsprechend sollten Sie den Inhaltsanfragetyp in Ihrem Player festlegen. In JavaScript würden Sie beispielsweise den Anfrage-Header `Content-Type` wie folgt festlegen:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
