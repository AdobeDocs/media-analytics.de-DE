---
title: Streaming-Mediensammlungs-API � Ereignisanfrage-Endpunkt
description: '"Was sind die Anforderungsparameter und Antworten der Media Collection API-Ereignisse?"'
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 92%

---

# Ereignisanfrage{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI-Parameter

`sid`: Die Sitzungs-ID, die von einer [Sitzungsanforderung](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) zurückgegeben wird.

## Anfrageinhalt

Der Anforderungstext muss im JSON-Format vorliegen und die gleiche Struktur aufweisen wie dieser Beispiel-Anforderungstext:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Obligatorisch)
   * `playhead`: Muss in Sekunden angegeben werden, es kann sich jedoch um einen Float-Wert handeln.
   * `ts`: Zeitstempel, der in Millisekunden angegeben werden muss.
* `eventType` (Obligatorisch)
* `params` (Optional)
* `customMetadata` (Optional, nur mit den Ereignistypen `adStart` und `chapterStart` senden)
* `qoeData` (Optional)

Eine Liste gültiger Ereignistypen für diese Version finden Sie unter [Ereignistypen und -beschreibungen.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Anzeigen-Tracking –** Sie können Anzeigen nur innerhalb einer`adBreak`* verfolgen.
>
>Wenn Anzeigen nicht durch `adBreakStart` und `adBreakComplete` eingeschlossen sind, werden die Ereignisse `adStart` und `adComplete` einfach ignoriert und die Werbedauer wird der Dauer des Hauptinhalts angerechnet. Das kann deutliche Auswirkungen auf die aggregierten Daten haben, die in Adobe Analytics zur Verfügung stehen.

## Antwort

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP-Antwortcodes

| HTTP-Antwortcode | Beschreibung | Client-Aktionen |
|---|---|---|
| **204** | **Kein Inhalt.** <br/><br/>Der Heartbeat-Aufruf war erfolgreich. | nicht angegeben |
| **400** | **Ungültige Anfrage.**<br/><br/>Die Anfrage hatte ein unzulässiges Format. | Überprüfen Sie die [JSON-Validierungs-Schemata](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) für den Anfragetyp. |
| **404** | **Nicht gefunden.** <br/><br/>Die Sitzungs-ID für die Mediensitzung wurde im Backend-Service nicht gefunden. | Die Client-Anwendung sollte die [Sitzungsanfrage](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API verwenden, um eine weitere Mediensitzung und Berichte dazu zu erstellen. |
| **410** | **Nicht mehr auffindbar.** <br/><br/>Die Mediensitzung wurde im Backend-Service gefunden, aber der Client kann einen Bericht mehr über die Aktivität bereitstellen. | Die Client-Anwendung sollte die [Sitzungsanfrage](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API verwenden, um eine weitere Mediensitzung und Berichte dazu zu erstellen. |
| **500** | **Serverfehler** | nicht angegeben |
