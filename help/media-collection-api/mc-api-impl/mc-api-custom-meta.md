---
title: Unterstützung benutzerspezifischer Metadaten
description: Unterstützung benutzerspezifischer Metadaten
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# Unterstützung benutzerspezifischer Metadaten {#custom-metadata-support}

Sie können benutzerdefinierte Schlüssel-Wert-Paare in den Ereignissen `sessionStart`, `chapterStart` und `adStart` festlegen. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

Der JSON-Schlüssel `customMetadata` sollte ein Objekt von Schlüssel-Wert-Paaren enthalten. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[MA Collection API-Ereignisse](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
