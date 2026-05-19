---
title: API-Konversion von Version 1.x zu 2.x
description: Informieren Sie sich über API-Referenzen, erforderliche Listen und optionale Tracking-APIs für die Versionen 1.x und 2.x des Media SDK.
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
exl-id: 8d06b7df-f246-49e6-aa58-91a9d6fa889a
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/szmY3oxBjmyZv4XrgYWnSCkpgPwgMDjAhWDjpbW4j1U
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 245
ht-degree: 95%

---

# Legacy API – Konvertierung von 1.x nach 2.x {#one-x-to-two-x-conv}

## API-Referenzen für Media SDK 2.x

* [Android-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [iOS-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Chromecast-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## Erforderliche Tracking*-APIs:

|  VHL 1.x  | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | K. A. |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | K. A. |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

Alle optionalen Tracking-APIs, z. B. Anzeigen, Kapitel, Bitratenänderungen, Änderungen der Abspielposition und Puffern, sind jetzt Teil einer einzigen `trackEvent`-API. Die [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent)-API empfängt einen Konstantenparameter, der den zu verfolgenden Ereignistyp angibt:

## Optionale trackEvent-APIs:

| VHL 1.x | VHL 2.x |
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
