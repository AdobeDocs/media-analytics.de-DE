---
title: 'Implementieren einer Ereignisanfrage '
description: Erfahren Sie, wie Sie den Ereignisanforderungs-Endpunkt für alle nachfolgenden Tracking-Aufrufe verwenden, nachdem Sie eine Sitzungs-ID erhalten haben.
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 100%

---

# Implementieren einer Ereignisanfrage {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Verwenden Sie die [Ereignisanforderung](../mc-api-ref/mc-api-events-req.md) für alle nachfolgenden Tracking-Aufrufe, nachdem Sie mithilfe der Sitzungsanforderung [eine Sitzungs-ID erhalten haben.](../mc-api-ref/mc-api-sessions-req.md) Geben Sie die Abspielleistenposition und den Zeitstempel, den Ereignistyp sowie sämtliche optionalen Parameter, die Sie hinzufügen möchten, im JSON-Text der Anforderung an.

Der JSON-Anforderungstext für die [Ereignisanforderung](../mc-api-ref/mc-api-events-req.md) weist dieselbe Struktur wie die Sitzungsanforderung auf. Sie sollten jedoch die [JSON-Validierungsschemas](../mc-api-ref/mc-api-json-validation.md) überprüfen, um mehr über die Parameteranforderungen und -typen zu erfahren.
