---
title: Einrichten von Roku 2.x für Streaming-Medien
description: Installieren und konfigurieren Sie Adobe Media SDK 2.x für Roku für reine Analytics-Streaming-Medienimplementierungen, einschließlich SceneGraph-Kanälen.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Einrichten von Roku 2.x für Streaming-Medien

Adobe Media SDK 2.x für Roku (`adbmobile.brs`) sendet Streaming-Mediendaten aus Roku-Kanälen, die in BrightScript geschrieben sind, direkt an Adobe Analytics. Es erfasst Zielgruppendaten über Audience Manager und misst die Interaktion durch Medienereignisse.

>[!NOTE]
>
>Auf dieser Seite wird die reine Analytics Media SDK 2.x für Roku behandelt. Für neue Implementierungen empfiehlt Adobe die [Roku Edge SDK](/help/implementation/edge/roku.md), die Daten zusätzlich zu Adobe Analytics für Customer Journey Analytics, Adobe Journey Optimizer und Real-Time CDP verfügbar macht.

* **Voraussetzungen**:
   * Schließen Sie die [Nur Analytics-Implementierung - Übersicht](overview.md) ab.
   * [Laden Sie die Media SDK für Roku herunter](/help/getting-started/download-sdks.md).
   * Fügen Sie eine API in Ihren Medien-Player ein, um Player-Ereignisse zu abonnieren, und eine API, die Player-Informationen wie den Mediennamen und die Abspielposition bereitstellt.

## Installieren des SDK

Der `AdobeMobileLibrary-2.*-Roku.zip` Download umfasst zwei Komponenten:

* `adbmobile.brs`: Die Bibliotheksdatei. Kopieren Sie es in das `pkg:/source/`-Verzeichnis Ihres Kanals.
* `ADBMobileConfig.json`: Die für Ihre App angepasste SDK-Konfigurationsdatei.

Kopieren Sie für SceneGraph-Kanäle auch `adbmobileTask.brs` und `adbmobileTask.xml` in Ihr `pkg:/components/`. Siehe [SceneGraph-Unterstützung](#scenegraph).

## Konfigurieren von ADBMobileConfig.json

Das Konfigurations-JSON verfügt über einen exklusiven `mediaHeartbeat` für Streaming-Medien. Fügen Sie `ADBMobileConfig.json` zu Ihrer Projektquelle hinzu und legen Sie die `mediaHeartbeat`-, `marketingCloud`- und `analytics` fest:

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| Konfigurationsparameter | Beschreibung |
| --- | --- |
| `server` | URL des Medien-Tracking-Endpunkts. Siehe [Nur Analytics-Implementierung - Übersicht](overview.md). |
| `publisher` | Eindeutige Kennung des Inhaltsherausgebers. |
| `channel` | Name des Inhaltsverteilungskanals. Wird als [Inhaltskanal“ &#x200B;](/help/implementation/variables/core/content-channel.md). |
| `ssl` | Ob SSL für Tracking-Aufrufe verwendet wird. |
| `ovp` | Name des Anbieters der Online-Videoplattform. |
| `sdkVersion` | Aktuelle Version Ihrer App oder SDK. |
| `playerName` | Name des Players. Wird als [Content-Player-Name“ &#x200B;](/help/implementation/variables/core/content-player-name.md). |

>[!IMPORTANT]
>
>Wenn `mediaHeartbeat` nicht richtig konfiguriert ist, wechselt das Medienmodul in einen Fehlerstatus und sendet keine Tracking-Aufrufe mehr. Stellen Sie sicher, dass Ihr `marketingCloud.org` `@AdobeOrg` enthält.

## SDK initialisieren und Nachrichten verarbeiten

Rufen Sie mit `ADBMobile()` eine Instanz der SDK ab. Der Besucher-ID-Service von Experience Cloud generiert eine Besucher-ID, die in allen Treffern enthalten ist.

>[!IMPORTANT]
>
>Rufen Sie alle 250 ms `processMessages` und `processMediaMessages` in Ihrer Hauptereignisschleife auf, damit der SDK Pings ordnungsgemäß sendet.

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| Methode | Beschreibung |
| --- | --- |
| `processMessages` | Übergibt Analytics-Ereignisse in der Warteschlange an die SDK. |
| `processMediaMessages` | Übergibt Medienereignisse in der Warteschlange an die SDK, einschließlich automatischer Pings. |

## Medien-Events tracken

Verfolgen Sie jedes Medienereignis, indem Sie seine SDK-Methode aufrufen. Auf der Registerkarte **Roku 2.x** auf jeder Seite [Ereignis](/help/implementation/events/overview.md) und [Variable](/help/implementation/variables/overview.md) finden Sie die genauen Aufrufe, Builder und Konstanten.

Eine typische Sitzung beginnt mit dem Erstellen eines Medienobjekts und dem Aufruf von `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

Die globalen `adb_media_init_*` erstellen die Medien-, Anzeigen-, Anzeigenunterbrechungs-, Kapitel- und QoS-Objekte, die von den Tracking-Aufrufen verwendet werden:

| Builder | Signatur |
| --- | --- |
| Medien | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| Anzeige | `adb_media_init_adinfo(name, id, position, length)` |
| Anzeigenunterbrechung | `adb_media_init_adbreakinfo(name, startTime, position)` |
| Kapitel | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

Standardmetadaten werden als assoziatives Array von `a.media.*` übergeben (die SDK definiert auch benannte Konstanten wie `MEDIA_VideoMetadataKeySHOW` für diese Schlüssel). Siehe die [Variablen](/help/implementation/variables/overview.md) für den Schlüssel, der jeder Dimension entspricht.

## Konfigurieren der Besucher-ID, des Datenschutzes und der Protokollierung von Experience Cloud

Die folgenden Methoden auf der `ADBMobile()` verwalten Identität, Datenschutz und Debugging:

| Methode | Beschreibung |
| --- | --- |
| `visitorMarketingCloudID()` | Ruft die Experience Cloud ID (ECID) ab. |
| `visitorSyncIdentifiers(identifiers)` | Legt zusätzliche Kunden-IDs für denselben Besucher fest. |
| `setAdvertisingIdentifier(rida)` | Legt die Roku-ID für Advertising (RIDA) fest. Abrufen mit der Roku-[`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic)-API. |
| `getAllIdentifiers()` | Gibt alle von SDK gespeicherten Kennungen aus, einschließlich Analytics-, Besucher-, Audience Manager- und benutzerdefinierter Kennungen. |
| `setPrivacyStatus(status)` | Legt den Datenschutzstatus fest. Übergeben Sie `adb.PRIVACY_STATUS_OPT_IN` oder `adb.PRIVACY_STATUS_OPT_OUT`. Siehe [Datenschutz](/help/implementation/opt-out-privacy.md). |
| `getPrivacyStatus()` | Gibt den aktuellen Datenschutzstatus zurück. |
| `setDebugLogging(flag)` | Aktiviert oder deaktiviert die Debug-Protokollierung. |
| `getDebugLogging()` | Gibt `true` zurück, wenn die Debugging-Protokollierung aktiviert ist. |

## SceneGraph-Unterstützung {#scenegraph}

Das Roku SceneGraph XML-Framework kann die veralteten BrightScript-SDK-APIs nicht direkt aufrufen, da der SDK Komponenten (z. B. Threads) verwendet, die für eine SceneGraph-App nicht verfügbar sind. Um diese Lücke zu schließen, stellt SDK einen Connector bereit, der eine SceneGraph-kompatible Instanz zurückgibt, die dieselben APIs verfügbar macht, sowie einen Rückrufmechanismus für APIs, die Daten zurückgeben.

Die Brücke besteht aus drei Teilen:

* **`adbmobileTask`-Knoten**: Ein SceneGraph-Aufgabenknoten, der SDK-APIs in einem Hintergrund-Thread ausführt und Daten an Ihre Szenen zurückgibt.
* **Connector-Instanz**: Schließt alle veralteten öffentlichen APIs ein und kommuniziert mit dem `adbmobileTask`.
* **`API_RESPONSE`Callback**: Das Feld, das Ihre App beobachtet, um Rückgabewerte von Getter-APIs zu erhalten.

So initialisieren Sie SDK in einem SceneGraph-Kanal:

1. `adbmobile.brs` in die Szene importieren:

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. Erstellen Sie den `adbmobileTask` Knoten, rufen Sie die Connector-Instanz ab und laden Sie die SceneGraph -Konstanten:

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. Registrieren Sie einen Callback, um Antwortobjekte für APIs zu erhalten, die Daten zurückgeben:

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

Die Connector-Instanz (`m.adbmobile`) macht dieselben Medienmethoden verfügbar wie die veraltete SDK (`mediaTrackSessionStart`, `mediaTrackPlay`, `mediaTrackPause`, `mediaTrackComplete`, `mediaTrackSessionEnd`, `mediaTrackError`, `mediaTrackEvent`, `mediaUpdatePlayhead` und `mediaUpdateQoS`), sodass die Aufrufe auf den Ereignis- und Variablenseiten auf die gleiche Weise funktionieren. Setter-APIs werden direkt aufgerufen; Getter-APIs geben ihre Werte über den `API_RESPONSE`-Callback zurück.

## Nächster Schritt

Sobald Ihre Implementierung abgeschlossen ist, können Sie [Berichte für reine Analytics-Implementierungen einrichten](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Übersicht über Ereignisse](/help/implementation/events/overview.md)
>* [Variablen - Übersicht](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
