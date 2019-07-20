---
seo-title: Tracking der Erlebnisqualität auf Roku
title: Tracking der Erlebnisqualität auf Roku
uuid: a 8 b 242 ab-da 3 c -4297-9 eef-f 0 b 9684 ef 56 a
translation-type: tm+mt
source-git-commit: 9d42a3a78d5f1812b41d83a5ae636d7a4bee2939

---


# Tracking der Erlebnisqualität auf Roku{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](../../sdk-implement/download-sdks.md)

## Implementierungs-QOS

1. Identify when the bitrate changes during media playback, and use the `mediaUpdateQoS` API to update the QoS info on the Media SDK.

   QoSObject-Variablen:

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie qos verfolgen.

   | Variable | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Aktuelle Bitrate | Ja |
   | `startupTime` | Startzeit | Ja |
   | `fps` | FPS-Wert | Ja |
   | `droppedFrames` | Anzahl der Dropped Frames | Ja |

   Beispiel:

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. When playback switches bitrates, call `trackEvent(BitrateChange)` to notify the Media SDK that the Bitrate changed.

   ```
   ADBMobile().trackMediaEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >You need to call `updateQoSObject` with the updated bitrate value.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Siehe [Übersicht](../../sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Die Verfolgung von Fehlern im Medienplayer stoppt die Medienverfolgungssitzung nicht. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

