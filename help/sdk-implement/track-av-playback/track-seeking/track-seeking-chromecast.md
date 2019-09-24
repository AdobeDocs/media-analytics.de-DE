---
seo-title: Suchen-Tracking in Chromecast
title: Suchen-Tracking in Chromecast
uuid: 8018e6c4-feed9-4de7-9eae-c720da55ad8c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suchen-Tracking in Chromecast{#track-seeking-on-chromecast}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen.[SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Suchverfolgungskonstanten

| Konstantenname | Beschreibung     |
|---|---|
| `SeekStart` | Konstante für die Verfolgung des Suchstartereignisses. |
| `SeekComplete` | Konstante für die Verfolgung des Suchabschlussereignisses. |

## Suche implementieren

1. Suchen Sie nach den Wiedergabesuchereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Suchstartereignis erhalten, verfolgen Sie die Suche mit dem `SeekStart`-Ereignis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart); 
   ```

1. Wenn Sie die Suchabschlussbenachrichtigung vom Medienplayer erhalten, verfolgen Sie das Ende der Suche mit dem `SeekComplete`-Ereignis: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete); 
   ```

Weitere Informationen finden Sie im Tracking-Szenario [VOD-Wiedergabe mit Suche im Hauptinhalt](/help/sdk-implement/tracking-scenarios/vod-seeking.md).
