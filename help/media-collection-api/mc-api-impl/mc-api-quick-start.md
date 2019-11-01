---
title: Schnellstart
description: null
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Schnellstart{#quick-start}

>[!TIP]
>
>Erfassen Sie die Anforderungsdaten, die zum Abschluss einer erfolgreichen [Sitzungsanfrage](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) beim Media Analytics (MA) Collection API-Back-End-Server erforderlich sind. Sie können Ihre Anfragedaten schnell überprüfen, indem Sie Anfragen manuell senden (mit `curl`, Postman usw.). So erhalten Sie umgehend Feedback dazu, ob in Ihrer Anfrage Probleme mit falschen Datentypen oder Informationen vorliegen. Verwenden Sie die [JSON-Validierungsschemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md), um zu überprüfen, ob Sie die richtigen Anfragedaten bereitstellen.

1. Sammeln Sie standardmäßige, erforderliche Adobe Analytics- und Besucherdaten, die Sie für die Ausführung von Experience Cloud-Anwendungen bereitstellen müssen:

   * Experience Cloud-Organisations-ID des Besuchers
   * Visitor Experience Cloud-Benutzer-ID
   * Analytics Report Suite-ID
   * Analytics-Tracking-Server-URL

1. Erstellen Sie ein JSON-Objekt für Ihren `sessions`-Anfrageinhalt, das die erforderlichen Daten für einen erfolgreichen Aufruf enthält. Beispiel:

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >Sie müssen die richtigen Datentypen im JSON-Anforderungstext verwenden. E.g., `analytics.enableSSL` requires a boolean, `media.length` is numeric, etc. You can check parameter types and mandatory versus optional requirements by checking the [JSON validation schemas.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Senden von Sitzungsanfragen an den API-Endpunkt für die MA-Sammlung. Wenn die Anfrage-Payload ungültig ist, ermitteln Sie das Problem und versuchen es erneut, bis Sie eine `201 Created`-Antwort erhalten. In this `curl` example, the JSON request body is in a file named `sample_data_session`:

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

Wenn die [Sitzungsanfrage](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) erfolgreich ist, erhalten Sie eine `201 Created`-Antwort ähnlich der oben aufgeführten. Die Antwort enthält eine Sitzungs-ID im Location-Header. Die Sitzungs-ID stellt eine wichtige Information in der Antwort dar, da sie für alle nachfolgenden Tracking-Aufrufe erforderlich ist. After a successful return of a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), you can confidently proceed with implementing video tracking using the MA API in your video player.
