---
title: Suchen-Tracking in Chromecast
description: Hier wird die Implementierung des Suchen-Trackings mit dem Media SDK in Chromecast beschrieben.
uuid: 8018e6c4-fed9-4de7-9eae-c720da55ad8c
exl-id: 03be8ed3-ae3a-4e9a-b667-0d9280a844a1
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '139'
ht-degree: 100%

---

# Suchen-Tracking in Chromecast {#track-seeking-on-chromecast}

>[!IMPORTANT]
>
>Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier die 1.x-Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Suchen-Tracking-Konstanten

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
