---
title: Roku Edge für Streaming-Medien einrichten
description: Konfigurieren Sie Adobe Experience Platform Roku SDK, um Streaming-Mediendaten an Edge Network zu senden.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%
---
# Roku Edge für Streaming-Medien einrichten

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript) erfasst Mediensessions-Daten in Ihrem Roku-Kanal und sendet sie an Edge Network. Roku ist im Code konfiguriert; es verwendet keine Tags.

* **Voraussetzungen**:
  * Abschließen der [Edge-Implementierungsübersicht](overview.md) (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).
  * Laden Sie die SDK von [GitHub-Versionen](https://github.com/adobe/aepsdk-roku/releases) herunter und fügen Sie sie Ihrem Kanal hinzu, wie in [Erste Schritte“ &#x200B;](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md).

## Konfigurieren von Roku Edge SDK für Media

Initialisieren Sie die SDK und legen Sie die Datenstrom- und Medienkonfiguration fest:

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

Öffnen Sie dann eine Sitzung mit `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>Senden Sie während der Wiedergabe mindestens einmal pro Sekunde ein `media.ping` mit dem neuesten Abspielkopfwert. Das Roku Edge SDK verlässt sich auf diese Pings, um ordnungsgemäß zu funktionieren.

Konfigurationsschlüssel und die vollständige API finden Sie in der [Roku Edge SDK API-Referenz](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md).

## Medien-Events tracken

Nachdem die Sitzung geöffnet ist, senden Sie jedes Medienereignis mit `sendMediaEvent`. Die **Payloads finden Sie auf der Registerkarte** Roku[&#x200B; auf jeder &#x200B;](/help/implementation/events/overview.md)- und [&#128279;](/help/implementation/variables/overview.md)-Seite.

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)
