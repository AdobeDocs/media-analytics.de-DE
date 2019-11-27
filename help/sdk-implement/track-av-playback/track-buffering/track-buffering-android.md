---
title: Puffer-Tracking in Android
description: Beschreibt das Tracking von Pufferereignissen in Android.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Puffer-Tracking in Android {#track-buffering-on-android}

>[!IMPORTANT]
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie die 1.x-Entwicklerhandbücher hier herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Puffer-Tracking-Konstanten

| Konstantenname | Beschreibung     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Konstante für die Verfolgung des Pufferstartereignisses |
| `MediaHeartbeat.Event.BufferComplete` | Konstante für die Verfolgung des Pufferabschlussereignisses |

## Implementieren der Pufferung

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
