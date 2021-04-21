---
title: Tracking der Pufferung mit JavaScript 3.x
description: Beschreibt das Tracking von Pufferereignissen in Browser-Anwendungen (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '115'
ht-degree: 100%

---

# Tracking der Pufferung mit JavaScript 3.x {#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 3.x-SDKs vornehmen. Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Puffer-Tracking-Konstanten

| Konstantenname | Beschreibung     |
|---|---|
| `BufferStart` | Konstante für die Verfolgung des Pufferstartereignisses |
| `BufferComplete` | Konstante für die Verfolgung des Pufferabschlussereignisses |

## Implementieren der Pufferung

1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Wenn Sie die Benachrichtigung zum Pufferabschluss vom Medienplayer erhalten, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Ereignis.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Puffern](/help/sdk-implement/tracking-scenarios/vod-buffering.md).
