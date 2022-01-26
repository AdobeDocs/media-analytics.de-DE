---
title: API-Konversion von Version 1.x zu 2.x
description: Informieren Sie sich über API-Referenzen, erforderliche Listen und optionale Tracking-APIs für die Versionen 1.x und 2.x des Media SDK.
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
exl-id: 8d06b7df-f246-49e6-aa58-91a9d6fa889a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---

# Konvertierung von API 1.x zu 2.x {#one-x-to-two-x-conv}

## API-Referenzen für Media SDK 2.x

* [Android-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [iOS-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [ Chromecast-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## Erforderliche Tracking*-APIs:

|  VHL 1.x  | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | nicht angegeben |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | nicht angegeben |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

Alle optionalen Tracking-APIs, z. B. Anzeigen, Kapitel, Bitratenänderungen, Änderungen der Abspielposition und Puffern, sind jetzt Teil einer einzigen `trackEvent`-API. Die [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent)-API empfängt einen Konstantenparameter, der den zu verfolgenden Ereignistyp angibt:

## Optionale trackEvent-APIs:

| VHL 1.x | VHL 2.x |
|---|---|
| Gültige `AdBreakInfo` in `VideoPlayerPlugin.getAdBreakInfo()` zurückgeben | `trackEvent(Event.AdBreakStart)` |
| Null in `VideoPlayerPlugin.getAdBreakInfo()` zurückgeben | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| Null in `VideoPlayerPlugin.getAdInfo()` zurückgeben | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| Null in `VideoPlayerPlugin.getChapterInfo()` zurückgeben | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |
