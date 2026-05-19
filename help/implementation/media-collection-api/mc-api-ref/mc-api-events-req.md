---
title: Streaming-Mediensammlungs-API ‐ Ereignisanfrage-Endpunkt
description: Was sind die Anforderungsparameter und Antworten der Media Collection API-Ereignisse?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 70%

---

# Ereignisanfrage{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI-Parameter

`sid`: Die Sitzungs-ID, die von einer [Sitzungsanfrage](mc-api-sessions-req.md) zurückgegeben wird.

## Anfrageinhalt

Der Anforderungstext muss im JSON-Format vorliegen und die gleiche Struktur aufweisen wie dieser Beispiel-Anforderungstext:

```json
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

Eine Liste der gültigen Ereignistypen und Implementierungsbeispiele pro SDK finden Sie unter [Ereignisübersicht](/help/implementation/events/overview.md).

>[!IMPORTANT]
>
>***Anzeigen-Tracking –** Sie können Anzeigen nur innerhalb einer`adBreak`* verfolgen.
>
>Wenn Anzeigen nicht durch `adBreakStart` und `adBreakComplete` eingeschlossen sind, werden die Ereignisse `adStart` und `adComplete` einfach ignoriert und die Werbedauer wird der Dauer des Hauptinhalts angerechnet. Das kann deutliche Auswirkungen auf die aggregierten Daten haben, die in Adobe Analytics zur Verfügung stehen.

## Antwort

```text
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
| **204** | **Kein Inhalt.** <br/><br/>Heartbeat-Aufruf war erfolgreich. | nicht angegeben |
| **400** | **Fehlerhafte Anfrage.** <br/><br/>Die Anfrage hatte ein falsches Format. | Überprüfen Sie die [JSON-Validierungs-Schemata](mc-api-json-validation.md) für den Anfragetyp. |
| **404** | **Nicht gefunden.** <br/><br/>Die Sitzungs-ID für die Mediensitzung wurde nicht im Back-End-Service gefunden. | Die Client-Anwendung sollte die [Sitzungsanfrage](mc-api-sessions-req.md)-API verwenden, um eine weitere Mediensitzung und Berichte dazu zu erstellen. |
| **410** | **nicht mehr vorhanden.** <br/><br/>Die Mediensitzung wurde im Back-End-Service gefunden, der Client kann jedoch keine Aktivitäten mehr darüber berichten. | Die Client-Anwendung sollte die [Sitzungsanfrage](mc-api-sessions-req.md)-API verwenden, um eine weitere Mediensitzung und Berichte dazu zu erstellen. |
| **500** | **Serverfehler** | nicht angegeben |
