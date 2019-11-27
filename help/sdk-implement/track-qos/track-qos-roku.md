---
title: Tracking der Erlebnisqualität auf Roku
description: Hier wird die Implementierung des Trackings der Erlebnisqualität (QoE, QoS) mit dem Media SDK in Roku beschrieben.
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracking der Erlebnisqualität auf Roku {#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementierung von QoS

1. Ermitteln Sie, wann sich die Bitrate während der Medienwiedergabe ändert, und verwenden Sie die `mediaUpdateQoS`-API, um die QoS-Informationen im Media SDK zu aktualisieren.

   QoSObject-Variablen:

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie die Erlebnisqualität (QoS) verfolgen.

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

1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie `trackEvent(BitrateChange)` auf, um dem Media SDK mitzuteilen, dass die Bitrate geändert wurde.

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >Sie müssen `updateQoSObject` mit dem aktualisierten Bitratenwert aufrufen.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. Wenn im Medienplayer ein Fehler auftritt und das Fehlerereignis der Player-API zur Verfügung steht, verwenden Sie `trackError()`, um die Fehlerinformationen zu erfassen. (Siehe [Übersicht](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Das Tracking von Fehlern im Medienplayer beendet die Medien-Tracking-Sitzung nicht. Wenn der Medienplayer-Fehler verhindert, dass die Wiedergabe fortgesetzt wird, müssen Sie sicherstellen, dass die Medien-Tracking-Sitzung geschlossen wird. Rufen Sie dazu `trackSessionEnd()` nach `trackError()` auf.

