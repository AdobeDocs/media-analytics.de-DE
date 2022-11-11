---
title: Streaming Media Analytics JSON-Validierungsschemas
description: Was sind JSON-Validierungs-Schemas für Streaming-Medien und wie werden sie verwendet, um die richtigen Parameter für den Anfragetext für jeden Ereignistyp zu ermitteln?
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 100%

---

# JSON-Validierungsschemas {#json-validation-schemas}

Das Media Analytics-Backend validiert die Anforderungsparameter für die verschiedenen Ereignistypen mithilfe von JSON-Validierungsschemas. Diese Schemas sind öffentlich verfügbar und ausschlaggebend für die in der MA-API verwendeten Parametertypen.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Weitere Informationen zur Verwendung der JSON-Validierungsschemata finden Sie unter [Validieren von Ereignisanfragen.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
