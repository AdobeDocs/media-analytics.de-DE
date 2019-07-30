---
seo-title: Unterstützung anwenderspezifischer Metadaten
title: Unterstützung anwenderspezifischer Metadaten
uuid: df 4109 dd -9 fca -4 c 33-a 7 d 5-8 e 6 eec 257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Unterstützung anwenderspezifischer Metadaten{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

The `customMetadata` JSON key should contain an object of key:value pairs. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[MA Collection API-Ereignisse](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

