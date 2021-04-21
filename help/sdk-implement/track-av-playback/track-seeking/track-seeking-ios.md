---
title: Suchen-Tracking in iOS
description: Hier wird die Implementierung des Suchen-Trackings mit dem Media SDK in iOS beschrieben.
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
exl-id: e8cb4962-2a14-4bfe-9a25-2405e503ba0b
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '123'
ht-degree: 100%

---

# Suchen-Tracking in iOS {#track-seeking-on-ios}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Suchen-Tracking-Konstanten

| Konstantenname | Beschreibung     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | Konstante für die Verfolgung des Suchstartereignisses. |
| `ADBMediaHeartbeatEventSeekComplete` | Konstante für die Verfolgung des Suchabschlussereignisses. |

## Suche implementieren

1. Suchen Sie nach den Wiedergabesuchereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Suchstartereignis erhalten, verfolgen Sie die Suche mit dem `SeekStart`-Ereignis:

   ```
   - (void)onSeekStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Wenn Sie die Benachrichtigung zum Suchabschluss vom Medienplayer erhalten, zeichnen Sie das Suchende mit dem `SeekComplete`-Ereignis auf:

   ```
   - (void)onSeekComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Suche im Hauptinhalt](/help/sdk-implement/tracking-scenarios/vod-seeking.md).
