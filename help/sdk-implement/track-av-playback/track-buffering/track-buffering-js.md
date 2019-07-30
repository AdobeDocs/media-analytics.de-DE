---
seo-title: Puffer-Tracking in JavaScript
title: Puffer-Tracking in JavaScript
uuid: c 380 cf 2 c -7729-4 d 4 a-a 4 da -581 bd 94 a 5896
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Puffer-Tracking in JavaScript{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Pufferverfolgungskonstanten

| Konstantenname | Beschreibung     |
|---|---|
| `BufferStart` | Konstante für die Verfolgung des Pufferstartereignisses |
| `BufferComplete` | Konstante für die Verfolgung des Pufferabschlussereignisses |

## Pufferung implementieren

1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis.

   ```js
   _onBufferStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
   };
   ```

1. Wenn Sie die Benachrichtigung zum Pufferabschluss vom Medienplayer erhalten, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Ereignis.

   ```js
   _onBufferComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
   };
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Puffern](/help/sdk-implement/tracking-scenarios/vod-buffering.md).
