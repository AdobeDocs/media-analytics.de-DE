---
seo-title: Puffer-Tracking in Chromecast
title: Puffer-Tracking in Chromecast
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Puffer-Tracking in Chromecast{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Pufferverfolgungskonstanten


| Konstantenname | Beschreibung     |
|---|---|
| `BufferStart` | Konstante für die Verfolgung des Pufferstartereignisses |
| `BufferComplete` | Konstante für die Verfolgung des Pufferabschlussereignisses |

## Implementierung der Pufferung

1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Wenn Sie vom Medienplayer die Benachrichtigung erhalten, dass die Pufferung abgeschlossen ist, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Event [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent) nach.

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Puffern](/help/sdk-implement/tracking-scenarios/vod-buffering.md).
