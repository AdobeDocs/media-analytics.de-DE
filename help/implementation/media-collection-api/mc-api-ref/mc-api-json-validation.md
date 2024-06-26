---
title: Streaming-Mediensammlungs-Add-on JSON-Validierungsschemas
description: Was sind JSON-Validierungs-Schemas für Streaming-Medien und wie werden sie verwendet, um die richtigen Parameter für den Anfragetext für jeden Ereignistyp zu ermitteln?
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 70%

---

# JSON-Validierungsschemas {#json-validation-schemas}

Das Backend der Streaming-Mediensammlungs-Add-On validiert die Anforderungsparameter für jeden Ereignistyp mithilfe von JSON-Validierungsschemas. Diese Schemas sind öffentlich verfügbar und ausschlaggebend für die in der MA-API verwendeten Parametertypen.

`GET https://{uri}/api/v1/schemas/{event-type}`

Weitere Informationen zur Verwendung der JSON-Validierungsschemata finden Sie unter [Validieren von Ereignisanfragen.](../mc-api-impl/mc-api-validate-reqs.md)
