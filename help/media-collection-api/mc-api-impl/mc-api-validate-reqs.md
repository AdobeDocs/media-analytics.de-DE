---
seo-title: Validieren von Ereignisanfragen
title: Validieren von Ereignisanfragen
uuid: 1 fc 92 f 21-b 510-4 c 96-8 ea 2-47 e 819 f 4 a 96 e
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Validieren von Ereignisanfragen{#validating-event-requests}

Der JSON-Anfrageinhalt für die einzelnen Ereignistypen muss am Backend mit JSON-Schemas validiert werden. Dem HTTP-Anfrageinhalt wird eine Fehlermeldung hinzugefügt, wenn die Validierung für einen API-Aufruf fehlschlägt.

JSON validation schemas for each event type are publicly accessible here: `{uri}/api/v1/schemas/{eventType}` (e.g., `{uri}/api/v1/schemas/sessionEnd`). Diese JSON-Validierungsschemata sind die absolute Stelle für die Ermittlung der richtigen Anforderungsparameter für jeden Ereignistyp.

Die Antwort auf eine Anfrage für das Validierungsschema `sessionStart` sieht beispielsweise ungefähr wie folgt aus (Formatierung zwecks Lesbarkeit leicht geändert):

```
HTTP/1.1 200 OK
Server: nginx/1.13.5
Date: Thu, 18 Jan 2018 15:44:50 GMT
Content-Type: application/json
Content-Length: 2716
Connection: keep-alive

{
  "$schema":"https://json-schema.org/draft-04/schema#",
  "id":"https://alpha.hb-api.omtrdc.net/api/v1/schemas/sessionStart",
  "definitions":
  {
    "playerTime":
    {
      "type":"object","properties":
      {
        "playhead":
        {"type":"number"},
        "ts":
        {"type":"integer"}
      },
      "required":["playhead","ts"],
      "additionalProperties":false
    },
    "eventType":
    {
      "type":"string",
      "enum":[
        "sessionStart",
        "play",
        "ping",
        "bufferStart",
        "pauseStart",
        "sessionComplete",
        "bitrateChange",
        "error",
        "adBreakStart",
        "adBreakComplete",
        "adStart",
        "adComplete",
        "adSkip",
        "sessionEnd"
      ]
    },
    "qoeData":
    {
      "type":"object","properties":
      {
        "media.qoe.bitrate":
        {"type":"integer"},
        "media.qoe.droppedFrames":
        {"type":"integer"},
        "media.qoe.framesPerSecond":
        {"type":"integer"},
        "media.qoe.timeToStart":
        {"type":"integer"}
      },
      "required":[],
      "additionalProperties":false
    },
    "customMetadata":
    {
      "type":"object",
      "patternProperties":
      {
        "^[a-zA-Z0-9_\\.]+$":
        {"type":"string"}
      },
      "additionalProperties":false
    },
    "sessionStart":
    {
      "properties":
      {
        "eventType":
        {"type":"string","enum":["sessionStart"]},
        "playerTime":
        {"$ref":"#/definitions/playerTime"},
        "params":
        {"type":"object",
          "properties":
          {
            "appInstallationId":
            {"type":"string"},
            "analytics.trackingServer":
            {"type":"string"},
            "analytics.reportSuite":
            {"type":"string"},
            <...>
            "visitor.marketingCloudOrgId"],
            "additionalProperties":false
          },
          "customMetadata":
          {"$ref":"#/definitions/customMetadata"},
          "qoeData":
          {"$ref":"#/definitions/qoeData"}
        },
        "required":["eventType","playerTime","params"],
        "additionalProperties":false
      }
    },
    "type":"object","$ref":"#/definitions/sessionStart"
  }
}
```

>[!NOTE]
>
>Überprüfung auf Sitzungsebene ist nicht möglich, da der Sitzungskontext in der Sammlungsebene nicht verfügbar ist.

