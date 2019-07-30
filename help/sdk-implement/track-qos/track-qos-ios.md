---
seo-title: Tracking der Erlebnisqualität auf iOS
title: Tracking der Erlebnisqualität auf iOS
uuid: cae 2 c 142-ed 39-4234-a 711-765 dcabc 5415
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracking der Erlebnisqualität auf iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Implementierungs-QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   QoSObject-Variablen:

   | Variable | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `bitrate` | Aktuelle Bitrate | Ja |
   | `startupTime` | Startzeit | Ja |
   | `fps` | FPS-Wert | Ja |
   | `droppedFrames` | Anzahl der Dropped Frames | Ja |

   >[!TIP]
   >
   >Diese Variablen sind nur erforderlich, wenn Sie planen, qos zu verfolgen.

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
   >Aktualisieren Sie das qos-Objekt und rufen Sie das Bitratenänderungsereignis bei jeder Bitratenänderung auf. So erhalten Sie möglichst präzise Daten.

