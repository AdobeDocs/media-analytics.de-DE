---
seo-title: Sitzungsanfrage
title: Sitzungsanfrage
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
translation-type: tm+mt
source-git-commit: f1c9f5f4cbcd4c043e1c7b4a5037c134b2bdd380

---


# Sitzungsanfrage{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI-Parameter

Keine

## Anfrageinhalt

Die Anforderungsstelle muss JSON sein und die gleiche Struktur wie die folgende MusteranforderungsTextstelle haben:

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
   * `playhead`: Muss in Sekunden angegeben werden, es kann sich jedoch um einen Float-Wert handeln.
   * `ts`: Zeitstempel, der in Millisekunden angegeben werden muss.
* `eventType` (Obligatorisch)

   **Gültiger Wert:**`sessionStart`
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

`Location:` header - Der `/api/v1/` Teil enthält die API-Version. Der nachfolgende Teil `[…]sessions/` ist die Sitzungs-ID.

## Antwortcodes

| HTTP-Antwortcode | Beschreibung |
|---|---|
| 201 | Sitzung erstellt |
| 400 | Unzulässige Anfrage |
| 500 | Serverfehler |

