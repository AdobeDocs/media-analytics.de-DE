---
seo-title: Implementieren einer Ereignisanfrage
title: Implementieren einer Ereignisanfrage
uuid: 3 bfa 313 c-ff 74-4 e 2 e-bbde -6 f 4 a 6221 d 85 b
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Implementieren einer Ereignisanfrage{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) Geben Sie im JSON-Hauptteil der Anforderung die Speicherposition und den Zeitstempel sowie den Ereignistyp und alle optionalen Parameter an, die Sie einbeziehen möchten.

The JSON request body for the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the Sessions request, however check the [JSON validation schemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) for parameter requirements and types.
