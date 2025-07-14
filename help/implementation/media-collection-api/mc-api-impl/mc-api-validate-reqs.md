---
title: Validieren von Ereignisanfragen
description: Erfahren Sie, wie Sie das JSON-Validierungsschema zur Validierung von Ereignisanfragen verwenden.
uuid: 1fc92f21-b510-4c96-8ea2-47e819f4a96e
exl-id: a78739da-9fc9-42e3-9181-1887fb3dd357
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 100%

---

# Validieren von Ereignisanfragen{#validating-event-requests}

Der JSON-Anfrageinhalt für die einzelnen Ereignistypen muss am Backend mit JSON-Schemas validiert werden. Dem HTTP-Anfrageinhalt wird eine Fehlermeldung hinzugefügt, wenn die Validierung für einen API-Aufruf fehlschlägt.

Die JSON-Validierungschemas für die verschiedenen Ereignistypen finden Sie unter `{uri}/api/v1/schemas/{eventType}` (z. B. `{uri}/api/v1/schemas/sessionEnd`). Diese JSON-Validierungsschemas sind ausschlaggebend für die Bestimmung der richtigen Anforderungstextparameter für die jeweiligen Ereignistypen.

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
>Die Validierung auf Sitzungsebene ist nicht möglich, da der Sitzungskontext nicht auf Sammlungsebene verfügbar ist.
