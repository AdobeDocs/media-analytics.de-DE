---
title: Tracking der Erlebnisqualität auf iOS
description: Hier wird die Implementierung des Trackings der Erlebnisqualität (QoE, QoS) mit dem Media SDK in iOS beschrieben.
uuid: cae2c142-ed39-4234-a711-765dcabc5415
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracking der Erlebnisqualität auf iOS {#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementierung von QoS

1. Ermitteln Sie, wann sich die Bitrate während der Medienwiedergabe ändert, und erstellen Sie die `MediaObject`-Instanz mithilfe der QoS-Informationen.

   QoSObject-Variablen:

   | Variable | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Aktuelle Bitrate | Ja |
   | `startupTime` | Startzeit | Ja |
   | `fps` | FPS-Wert | Ja |
   | `droppedFrames` | Anzahl der Dropped Frames | Ja |

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie die Servicequalität (QoS) verfolgen möchten.

   Erstellung von QoS-Objekten:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Stellen Sie sicher, dass die `getQoSObject`-Methode die neuesten QoS-Informationen zurückgibt.
1. Wenn sich die Bitrate der Wiedergabe ändert, rufen Sie das `BitrateChange`-Ereignis in der Media Heartbeat-Instanz auf:

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Aktualisieren Sie das QoS-Objekt und rufen Sie das Ereignis zur Bitratenänderung bei jeder Bitratenänderung auf. So erhalten Sie möglichst präzise Daten.

