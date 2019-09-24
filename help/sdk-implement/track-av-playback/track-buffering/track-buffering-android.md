---
seo-title: Puffer-Tracking in Android
title: Puffer-Tracking in Android
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Puffer-Tracking in Android{#track-buffering-on-android}

>[!IMPORTANT]
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDks.](/help/sdk-implement/download-sdks.md)

## Pufferverfolgungskonstanten

| Konstantenname | Beschreibung     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Konstante für die Verfolgung des Pufferstartereignisses |
| `MediaHeartbeat.Event.BufferComplete` | Konstante für die Verfolgung des Pufferabschlussereignisses |

## Implementierung der Pufferung

1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis:

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. Wenn Sie die Benachrichtigung zum Pufferabschluss vom Medienplayer erhalten, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Ereignis:

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Puffern](/help/sdk-implement/tracking-scenarios/vod-buffering.md).
