---
title: Roku für Streaming-Medien einrichten
description: Konfigurieren Sie Adobe Experience Platform Roku SDK, um Streaming-Mediendaten an Edge Network zu senden.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Roku für Streaming-Medien einrichten

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript) erfasst Mediensessions-Daten in Ihrem Roku-Kanal und sendet sie an Edge Network. Roku ist im Code konfiguriert; es verwendet keine Tags.

* **Voraussetzungen**:
   * Abschließen der [Edge-Implementierungsübersicht](overview.md) (Schema, Datensatz, Datenstrom mit aktiviertem [!UICONTROL Media Analytics]).
   * Laden Sie die SDK von [GitHub-Versionen](https://github.com/adobe/aepsdk-roku/releases) herunter und fügen Sie sie Ihrem Kanal hinzu, wie in [Erste Schritte“ &#x200B;](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md).

## Konfigurieren von AEP Roku SDK für Media

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
>Senden Sie während der Wiedergabe mindestens einmal pro Sekunde ein `media.ping` mit dem neuesten Abspielkopfwert. Der AEP Roku SDK ist auf diese Pings angewiesen, um ordnungsgemäß zu funktionieren.

Konfigurationsschlüssel und die vollständige API finden Sie in der [AEP Roku SDK API-Referenz](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md).

## Medien-Events tracken

Nachdem die Sitzung geöffnet ist, senden Sie jedes Medienereignis mit `sendMediaEvent`. Auf der **Roku**-Registerkarte auf jeder [Ereignis](/help/implementation/events/overview.md) und [Variable](/help/implementation/variables/overview.md)-Seite finden Sie die genauen Payloads.

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für Edge-Implementierungen einrichten](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)
