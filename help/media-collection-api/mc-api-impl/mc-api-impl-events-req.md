---
title: Implementieren einer Ereignisanfrage
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementieren einer Ereignisanfrage{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Geben Sie die Position und den Zeitstempel der Abspielleiste, den Ereignistyp und alle optionalen Parameter, die Sie einbeziehen möchten, im JSON-Hauptteil der Anforderung an.

The JSON request body for the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the Sessions request, however check the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for parameter requirements and types.
