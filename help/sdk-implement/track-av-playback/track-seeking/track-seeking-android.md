---
seo-title: Suchen-Tracking in Android
title: Suchen-Tracking in Android
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suchen-Tracking in Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Suchverfolgungskonstanten

| Konstantenname | Beschreibung     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Konstante für die Verfolgung des Suchstartereignisses. |
| `MediaHeartbeat.Event.SeekComplete` | Konstante für die Verfolgung des Suchabschlussereignisses. |

## Suche implementieren

1. Suchen Sie nach den Wiedergabesuchereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Suchstartereignis erhalten, verfolgen Sie die Suche mit dem `SeekStart`-Ereignis:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. Wenn Sie die Benachrichtigung zum Suchabschluss vom Medienplayer erhalten, zeichnen Sie das Suchende mit dem `SeekComplete`-Ereignis auf:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Suche im Hauptinhalt](/help/sdk-implement/tracking-scenarios/vod-seeking.md).
