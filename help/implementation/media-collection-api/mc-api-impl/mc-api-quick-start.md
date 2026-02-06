---
title: Streaming-Mediensammlungs-API - Schnellstart
description: Erste Schritte mit der Streaming Media-API. Erfahren Sie, wie Sie Ihre Anfragedaten schnell überprüfen können.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 97%

---

# Schnellstart{#quick-start}

>[!TIP]
>
>Erfassen Sie die Anforderungsdaten, die zum Abschluss einer erfolgreichen [Sitzungsanforderung](../mc-api-ref/mc-api-sessions-req.md) beim Backend-Server der Media Analytics (MA) Collection API erforderlich sind. Sie können Ihre Anfragedaten schnell überprüfen, indem Sie Anfragen manuell senden (mit `curl`, Postman usw.). Auf diese Weise erhalten Sie sofort Rückmeldungen darüber, ob Ihre Anfrage Probleme mit falschen Datentypen oder falschen Informationen enthält. Überprüfen Sie mithilfe der [JSON-Validierungs-Schemata](../mc-api-ref/mc-api-json-validation.md), ob Sie die richtigen Anfragedaten bereitstellen.

1. Erfassen Sie die standardmäßig erforderlichen Adobe Analytics- und Besucherdaten, die Sie zur Ausführung einer Experience Cloud-Anwendung bereitstellen müssen:

   * Experience Cloud-Org-ID des Besuchers
   * Experience Cloud-Benutzer-ID des Besuchers
   * Analytics-Report Suite-ID
   * Analytics-Tracking-Server-URL

1. Erstellen Sie ein JSON-Objekt für Ihren `sessions`-Anfrageinhalt, das die erforderlichen Daten für einen erfolgreichen Aufruf enthält. Beispiel:

   ```json
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
   >Sie müssen die richtigen Datentypen im JSON-Anforderungstext verwenden. So erfordert `analytics.enableSSL` beispielsweise einen booleschen Wert, `media.length` einen numerischen usw. Sie können die Parametertypen sowie ihre Erforderlichkeit anhand der [JSON-Validierungsschemas](mc-api-validate-reqs.md) überprüfen.

1. Senden Sie Sitzungsanforderungen an den MA Collection API-Endpunkt. Wenn die Anfrage-Payload ungültig ist, ermitteln Sie das Problem und versuchen es erneut, bis Sie eine `201 Created`-Antwort erhalten. In diesem `curl`-Beispiel befindet sich der JSON-Anforderungstext in einer Datei namens `sample_data_session`:

   ```sh
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

Wenn die [Sitzungsanfrage](../mc-api-ref/mc-api-sessions-req.md) erfolgreich ist, erhalten Sie eine `201 Created`-Antwort ähnlich der oben aufgeführten. Die Antwort enthält eine Sitzungs-ID in der Kopfzeile „Position“. Die Sitzungs-ID ist eine entscheidende Information in der Antwort, da sie für alle nachfolgenden Tracking-Aufrufe erforderlich ist. Nach der erfolgreichen Rückgabe einer [Sitzungsanforderung](../mc-api-ref/mc-api-sessions-req.md) können Sie mit der Implementierung des Video-Trackings mithilfe der MA-API in Ihrem Videoplayer fortfahren.
