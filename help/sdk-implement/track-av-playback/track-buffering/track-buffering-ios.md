---
seo-title: Puffer-Tracking in iOS
title: Puffer-Tracking in iOS
uuid: 4 f 4 db 23 a -489 b -4 b 41-bb 6 e -393 ec 64 d 52 a 2
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Puffer-Tracking in iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](../../../sdk-implement/download-sdks.md)

## Pufferverfolgungskonstanten


| Konstantenname | Beschreibung     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Konstante für die Verfolgung des Pufferstartereignisses |
| `ADBMediaHeartbeatEventBufferComplete` | Konstante für die Verfolgung des Pufferabschlussereignisses |

## Pufferung implementieren

1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis:

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Wenn Sie die Benachrichtigung zum Pufferabschluss vom Medienplayer erhalten, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Ereignis:

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Puffern](../../../sdk-implement/tracking-scenarios/vod-buffering.md).
