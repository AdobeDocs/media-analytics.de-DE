---
title: Implementieren einer Ereignisanfrage
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementieren einer Ereignisanfrage {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Verwenden Sie die [Ereignisanforderung](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) für alle nachfolgenden Tracking-Aufrufe, nachdem Sie mithilfe der Sitzungsanforderung [ eine Sitzungs-ID erhalten haben.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Geben Sie die Abspielleistenposition und den Zeitstempel, den Ereignistyp sowie sämtliche optionalen Parameter, die Sie hinzufügen möchten, im JSON-Text der Anforderung an.

Der JSON-Anforderungstext für die [Ereignisanforderung](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) weist dieselbe Struktur wie die Sitzungsanforderung auf. Sie sollten jedoch die [JSON-Validierungsschemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) überprüfen, um mehr über die Parameteranforderungen und -typen zu erfahren.
