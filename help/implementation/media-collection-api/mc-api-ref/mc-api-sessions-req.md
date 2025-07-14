---
title: Streaming-Mediensammlungs-API – Sitzungsanfrage-Endpunkt
description: Was sind die Anforderungsparameter und Antworten der Media Collection API-Sitzungen?
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 90%

---

# Sitzungsanfrage {#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI-Parameter

Keine

## Anfrageinhalt

Der Anforderungstext muss im JSON-Format vorliegen und die gleiche Struktur aufweisen wie dieser Beispiel-Anforderungstext:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (Obligatorisch)
   * `playhead` – Wenn der Inhalt live ist, muss der Abspielkopf sich an der aktuellen Sekunde des Tages befinden, 0 &lt;= Abspielkopf &lt; 86400. Wenn der Inhalt aufgezeichnet wird, muss der Abspielkopf sich an der aktuellen Sekunde des Inhalts befinden, 0 &lt;= Abspielkopf &lt; Inhaltsdauer. Der Wert kann eine Gleitkommazahl sein.
   * `ts` – Zeitstempel; muss in Millisekunden angegeben werden; Koordinierte Weltzeit (UTC).
* `eventType` (Obligatorisch)

  **Gültiger Wert:** `sessionStart`
* `params` (Obligatorisch)
* `customMetadata` (Optional)
* `qoeData` (Optional)

## Antwort

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:`-Header: Der Teil `/api/v1/` enthält die API-Version. Der nachfolgende Teil `[…]sessions/` ist die Sitzungs-ID.

## Antwortcodes

| HTTP-Antwortcode | Beschreibung |
|---|---|
| 201 | Sitzung erstellt |
| 400 | Ungültige Anfrage |
| 500 | Server-Fehler |
