---
seo-title: Schnellstart
title: Schnellstart
uuid: ca 20 bad 4-2 c 8 f -406 b -833 e-b 4883 a 9 aa 534
translation-type: tm+mt
source-git-commit: 654aaef5d816e75429975d04c4e81ad4d4b6f706

---


# Schnellstart{#quick-start}

>[!TIP]
>
>Gather the request data necessary for completing a successful [Session request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) to the Media Analytics (MA) Collection API back-end server. Sie können Ihre Anfragedaten schnell überprüfen, indem Sie Anfragen manuell senden (mit `curl`, Postman usw.). So erhalten Sie umgehend Feedback dazu, ob in Ihrer Anfrage Probleme mit falschen Datentypen oder Informationen vorliegen. Verwenden Sie die [JSON-Validierungsschemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md), um zu überprüfen, ob Sie die richtigen Anfragedaten bereitstellen.

1. Sammeln Sie standardmäßige, erforderliche Adobe Analytics- und Besucherdaten, die Sie für die Ausführung von Experience Cloud-Anwendungen bereitstellen müssen:

   * Experience Cloud-Organisations-ID des Besuchers
   * Besucher-ID für Besucher-Experience Cloud
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
   >Sie müssen im JSON-Anforderungstext die richtigen Datentypen verwenden. `analytics.enableSSL` Erfordert z. B. ein boolesches, `media.length` es ist numerisch usw. You can check parameter types and mandatory versus optional requirements by checking the [JSON validation schemas.](../../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Senden Sie Anforderungen an den MA Collection API-Endpunkt. Wenn die Anfrage-Payload ungültig ist, ermitteln Sie das Problem und versuchen es erneut, bis Sie eine `201 Created`-Antwort erhalten. In this `curl` example, the JSON request body is in a file named `sample_data_session`:

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

Wenn die [Sitzungsanfrage](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) erfolgreich ist, erhalten Sie eine `201 Created`-Antwort ähnlich der oben aufgeführten. Die Antwort enthält eine Sitzungs-ID im Location-Header. Die Sitzungs-ID stellt eine wichtige Information in der Antwort dar, da sie für alle nachfolgenden Tracking-Aufrufe erforderlich ist. After a successful return of a [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md), you can confidently proceed with implementing video tracking using the MA API in your video player.
