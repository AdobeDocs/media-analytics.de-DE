---
title: Einrichten der Media Edge-API für Streaming-Medien
description: Senden Sie Streaming-Mediendaten mithilfe der Media Edge-API direkt an Edge Network.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%
---
# Einrichten der Media Edge-API für Streaming-Medien

Wenn Sie Web SDK, Mobile SDK oder Roku Edge SDK nicht verwenden können (z. B. auf einer benutzerdefinierten oder nicht unterstützten Laufzeit), können Sie Streaming-Mediendaten mit der Media Edge-API direkt an Edge Network senden. Die API verwendet RESTful-HTTP-Aufrufe und kann vollständig angepasst werden.

* **Voraussetzungen**: Abschließen der [Übersicht über die Edge](overview.md)Implementierung (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).

## Senden von Medienereignissen an Edge Network

Medienereignisse werden an die `/ee/va/v1/`-Endpunkte gesendet und vom `configId` Abfrageparameter in Ihren Datenstrom verschlüsselt. Beispielsweise beginnt eine Sitzung mit einem POST-Test, um Folgendes zu `sessionStart`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

Die Antwort gibt die Sitzungs-ID zurück, die alle nachfolgenden Ereignisse enthalten müssen. Den vollständigen Endpunktsatz, die Anfrage-/Antwortformate und die OpenAPI-Spezifikation finden Sie in der [Media Edge API-Referenz](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

## Medien-Events tracken

Die genauen Payloads finden Sie auf **Registerkarte** Media Edge[&#x200B; auf jeder &#x200B;](/help/implementation/events/overview.md)- und [&#128279;](/help/implementation/variables/overview.md).

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Media Edge-API-Referenz](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)
