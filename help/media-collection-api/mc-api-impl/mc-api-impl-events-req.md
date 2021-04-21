---
title: Implementieren einer Ereignisanfrage
description: Implementieren einer Ereignisanfrage
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 100%

---

# Implementieren einer Ereignisanfrage {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Verwenden Sie die [Ereignisanforderung](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) für alle nachfolgenden Tracking-Aufrufe, nachdem Sie mithilfe der Sitzungsanforderung [eine Sitzungs-ID erhalten haben.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Geben Sie die Abspielleistenposition und den Zeitstempel, den Ereignistyp sowie sämtliche optionalen Parameter, die Sie hinzufügen möchten, im JSON-Text der Anforderung an.

Der JSON-Anforderungstext für die [Ereignisanforderung](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) weist dieselbe Struktur wie die Sitzungsanforderung auf. Sie sollten jedoch die [JSON-Validierungsschemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) überprüfen, um mehr über die Parameteranforderungen und -typen zu erfahren.
