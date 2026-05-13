---
title: Erfahren Sie, wie Sie die Erlebnisqualität in iOS verfolgen können.
description: Erfahren Sie mehr über die Implementierung des Trackings der Erlebnisqualität (QoE, QoS) mit Media SDK in iOS.
uuid: cae2c142-ed39-4234-a711-765dcabc5415
exl-id: 7f01e6eb-95bd-4e3d-93d0-8a2e68323313
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/37GAel-VlcHz-jmbicc1WphVs0y7-E8UDbBInmMT9LQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 159
ht-degree: 89%

---

# Nachverfolgen der Erlebnisqualität auf iOS{#track-quality-of-experience-on-ios}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Implementieren von QoS

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
