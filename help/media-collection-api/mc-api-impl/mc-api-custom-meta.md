---
title: Unterstützung anwenderspezifischer Metadaten
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Unterstützung anwenderspezifischer Metadaten{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

The `customMetadata` JSON key should contain an object of key:value pairs. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[API-Ereignisse zur MA-Sammlung](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

