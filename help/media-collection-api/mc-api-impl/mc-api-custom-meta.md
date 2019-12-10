---
title: Unterstützung benutzerspezifischer Metadaten
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Unterstützung benutzerspezifischer Metadaten {#custom-metadata-support}

Sie können benutzerdefinierte Schlüssel-Wert-Paare in den Ereignissen `sessionStart``chapterStart` und `adStart` festlegen. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

Der JSON-Schlüssel `customMetadata` sollte ein Objekt von Schlüssel-Wert-Paaren enthalten. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[MA Collection API-Ereignisse](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

