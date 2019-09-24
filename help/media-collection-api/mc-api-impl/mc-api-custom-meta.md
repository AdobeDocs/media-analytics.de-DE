---
seo-title: Unterstützung anwenderspezifischer Metadaten
title: Unterstützung anwenderspezifischer Metadaten
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Unterstützung anwenderspezifischer Metadaten{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

The `customMetadata` JSON key should contain an object of key:value pairs. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[API-Ereignisse zur MA-Sammlung](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

