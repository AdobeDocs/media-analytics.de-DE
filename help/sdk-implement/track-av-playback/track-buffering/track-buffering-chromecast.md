---
title: Puffer-Tracking in Chromecast
description: Beschreibt das Tracking von Pufferereignissen in Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Puffer-Tracking in Chromecast {#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Puffer-Tracking-Konstanten


| Konstantenname | Beschreibung     |
|---|---|
| `BufferStart` | Konstante für die Verfolgung des Pufferstartereignisses |
| `BufferComplete` | Konstante für die Verfolgung des Pufferabschlussereignisses |

## Implementieren der Pufferung

1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Wenn Sie vom Medienplayer die Benachrichtigung erhalten, dass die Pufferung abgeschlossen ist, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Event [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent) nach.

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Puffern](/help/sdk-implement/tracking-scenarios/vod-buffering.md).
