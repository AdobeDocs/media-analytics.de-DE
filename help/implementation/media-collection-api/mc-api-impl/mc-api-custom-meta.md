---
title: Unterstützung benutzerspezifischer Metadaten
description: Erfahren Sie, wie Sie benutzerdefinierte Schlüssel-Wert-Paare für die Ereignisse sessionStart, chapterStart und adStart bereitstellen.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 62%

---

# Unterstützung benutzerspezifischer Metadaten{#custom-metadata-support}

Sie können benutzerdefinierte Schlüssel:valuePaare für die `sessionStart`-, `chapterStart`- und `adStart` bereitstellen. Diese Informationen müssen im JSON-Schlüssel `customMetadata` neben dem `params`-Schlüssel bereitgestellt werden.

Der `customMetadata` JSON-Schlüssel sollte ein Objekt von Schlüssel:valuePaaren enthalten. Der Schlüssel darf nur alphanumerische Zeichen, Unterstriche und Punkte enthalten.

[MA Collection API-Ereignisse](../mc-api-ref/mc-api-events-req.md)

## Beispiel

Derzeit können Sie ein `sessionStart`-Ereignis mit dem folgenden Schlüssel-:value-Paar senden:

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
