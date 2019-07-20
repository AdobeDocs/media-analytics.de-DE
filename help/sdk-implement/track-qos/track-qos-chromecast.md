---
seo-title: Tracking der Erlebnisqualität auf Chromecast
title: Tracking der Erlebnisqualität auf Chromecast
uuid: d 0 cdc 8 cd -4 db 0-45 ef -9470-1 cba 3996305 b
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Tracking der Erlebnisqualität auf Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](../../sdk-implement/download-sdks.md)

## Überblick {#section_DDB8DFA47C5744AB9A04392AD5959BF7}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Sie können die Media Player-API verwenden, um die Variablen zu identifizieren, die mit Servicequalitäts- und Fehlerverfolgung zusammenhängen.

## Player events {#player-events}

### Bei allen Ereignissen zu Bitratenänderungen

* Erstellen/aktualisieren Sie die QoS-Objektinstanz für die Wiedergabe, `qosObject`.
* Aufruf    `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Bei Player-Fehlern

Aufruf    `trackError(“media error id”);`

## Implementierung {#section_3B8EBEB167624D0481E8AF4761F83047}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **QoSObject-Variablen:**

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie planen, qos zu verfolgen.

   | Variable | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Aktuelle Bitrate | Ja |
   | `startupTime` | Startzeit | Ja |
   | `fps` | FPS-Wert | Ja |
   | `droppedFrames` | Anzahl der Dropped Frames | Ja |

   **Erstellung von QoS-Objekten:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie das `BitrateChange`-Ereignis in der Media Heartbeat-Instanz auf: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Aktualisieren Sie das qos-Objekt und rufen Sie das Bitratenänderungsereignis bei jeder Bitratenänderung auf. So erhalten Sie möglichst präzise Daten.

1. Stellen Sie sicher, dass die `getQoSObject()`-Methode die neuesten QoS-Informationen zurückgibt.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Siehe [Übersicht](../../sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Die Verfolgung von Fehlern im Medienplayer stoppt die Medienverfolgungssitzung nicht. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

