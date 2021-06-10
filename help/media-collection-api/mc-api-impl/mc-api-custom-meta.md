---
title: Unterstützung benutzerspezifischer Metadaten
description: Unterstützung benutzerspezifischer Metadaten
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
source-git-commit: 962bb8b6859ca8964efcb2f3ba0dc566a5e24c3e
workflow-type: ht
source-wordcount: '115'
ht-degree: 100%

---

# Unterstützung benutzerspezifischer Metadaten {#custom-metadata-support}

Sie können benutzerdefinierte Schlüssel-Wert-Paare in den Ereignissen `sessionStart`, `chapterStart` und `adStart` festlegen. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

Der JSON-Schlüssel `customMetadata` sollte ein Objekt von Schlüssel-Wert-Paaren enthalten. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[MA Collection API-Ereignisse](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## Beispiel

Derzeit können Sie ein `sessionStart`-Ereignis mit dem folgenden Schlüssel-Wert-Paar senden:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Für die obige Konfiguration werden die folgenden Berichtsdaten an Analytics gesendet:

`c.a.media.channel=channel-2`

### Empfehlung

Es wird empfohlen, einen separaten Namespace für benutzerdefinierte Metadaten zu verwenden. Beispiel:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

Im empfohlenen Beispiel lauten die Berichtsdaten für benutzerdefinierte Metadaten, die an Analytics gesendet werden, wie folgt:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
