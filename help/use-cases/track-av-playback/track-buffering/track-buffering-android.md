---
title: Erfahren Sie, wie Sie Nachverfolgen der Pufferung auf Android durchführen.
description: Erfahren Sie, wie Sie Pufferereignisse in Android verfolgen.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 100%

---

# Nachverfolgen der Pufferung auf Android{#track-buffering-on-android}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

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

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Puffern](/help/use-cases/tracking-scenarios/vod-buffering.md).
