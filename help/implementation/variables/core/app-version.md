---
title: Anwendungsversion
description: Konfigurieren Sie die Versionszeichenfolge Ihrer Media Player-Anwendung.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 2%

---


# Anwendungsversion

>[!BEGINSHADEBOX]

*Auf dieser Seite wird die Datenerfassung für die Variable **App-Version**behandelt. Siehe [App-Version](/help/reporting/dimensions/app-version.md) für die entsprechende Reporting-Dimension.*

>[!ENDSHADEBOX]

Die Anwendungsversionsvariable identifiziert die Version Ihrer Media Player-Anwendung. Legen Sie ihn bei der Initialisierung von SDK einmal fest. Der Wert wird automatisch in jeder nachfolgenden Anfrage zum Sitzungsstart enthalten. Verwenden Sie eine Versionszeichenfolge, die dem Versionszyklus Ihrer Anwendung entspricht (z. B. `"2.1.0"` oder `"prod-YYYY-03-15"`).

>[!NOTE]
>
>In diesem Feld wird die Version Ihres **Media Player-Programms** erfasst, nicht die SDK-Bibliothek von Adobe. Adobes eigene SDK-Bibliotheksversion wird automatisch als separates internes Feld erfasst.

| Eigenschaft | Wert |
| --- | --- |
| **XDM-Sammlungsfeld** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Mediensammlungs-API-Parameter** | `media.sdkVersion` |
| **Erforderlich** | Nein |
| **Gesendet mit** | [Sitzungsstart](/help/implementation/events/session/session-start.md) |

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Legen Sie beim Aufrufen von [`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia) `appVersion` im `streamingMedia`-Konfigurationsobjekt fest:

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

Legen Sie `edgeMedia.appVersion` in der App-Konfiguration fest, bevor Sie den Medien-Tracker initialisieren:

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

Legen Sie `edgeMedia.appVersion` in der App-Konfiguration fest, bevor Sie den Medien-Tracker initialisieren:

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku Edge]

Legen Sie die App-Version in der SDK-Konfiguration mithilfe von `ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION` fest:

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB Media Edge-API]

Fügen Sie `appVersion` in das `sessionDetails` der Anfrage [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) ein:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Legen Sie `appVersion` für das `MediaConfig` fest, bevor Sie `ADB.Media.configure` aufrufen:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

Legen Sie `sdkVersion` im Abschnitt `mediaHeartbeat` der ADBMobile-Konfiguration fest. In diesem Feld wird die Version der Player-Anwendung erfasst, nicht die SDK-Bibliotheksversion von Chromecast.

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB Roku 2.x]

`sdkVersion` Sie im `mediaHeartbeat` Abschnitt von `ADBMobileConfig.json`. In diesem Feld wird die Version der Player-Anwendung erfasst, nicht die SDK-Bibliotheksversion von Roku 2.x:

```json
"mediaHeartbeat": {
  "sdkVersion": "2.1.0"
}
```

>[!TAB Media Collection API]

Fügen Sie `media.sdkVersion` in das `params` Ihrer `sessionStart` POST-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

Die vollständige Anfragestruktur finden Sie [Referenz zur ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)-API für Mediensammlungs-Sitzungen).

>[!ENDTABS]
