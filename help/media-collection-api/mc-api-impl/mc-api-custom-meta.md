---
seo-title: Unterstützung anwenderspezifischer Metadaten
title: Unterstützung anwenderspezifischer Metadaten
uuid: df 4109 dd -9 fca -4 c 33-a 7 d 5-8 e 6 eec 257527
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Unterstützung anwenderspezifischer Metadaten{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

The `customMetadata` JSON key should contain an object of key:value pairs. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[MA Collection API-Ereignisse](../mc-api-ref/mc-api-events-req.md)

