---
title: Code-Vergleich von v1.x mit v2.x
description: Erfahren Sie mehr über den Unterschied zwischen Code in den Versionen 1.x und 2.x des Media SDK.
uuid: 9f0a1660-2100-446d-ab75-afdf966478b3
exl-id: c2324c6a-329f-44e2-bea0-9d43ef9c6ef7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 100%

---

# Codevergleich: 1.x gegenüber 2.x {#code-comparison-x-to-x}

Alle Konfigurationsparameter und Tracking-APIs wurden in den `MediaHeartbeats`- und `MediaHeartbeatConfig`-Klassen zusammengeführt.

**Konfigurations-API-Änderungen:**

* `AdobeHeartbeatPluginConfig.sdk`: Umbenannt in `MediaConfig.appVersion`.
* `MediaHeartbeatConfig.playerName`: Wird jetzt über `MediaHeartbeatConfig` statt über `VideoPlayerPluginDelegate` festgelegt.
* (Nur für JavaScript) `AppMeasurement`-Instanz: Wird jetzt über den `MediaHeartbeat`-Constructor gesendet.

**Änderungen von Konfigurationseigenschaften:**

* `sdk`: Umbenannt in `appVersion`.
* `publisher`: Entfernt. Stattdessen wird die Experience Cloud-Organisations-ID als Publisher verwendet.
* `quiteMode` - Entfernt

**Links zu 1.x- und 2.x-Beispielplayern:**

* [1.x-Beispiel-Player ](https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58)
* [2.x-Beispiel-Player ](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/2.x/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L47)

In den folgenden Abschnitten finden Sie einen Codevergleich zwischen 1.x und 2.x. Dieser Vergleich deckt die Initialisierung, Core-Wiedergabe, Anzeigenwiedergabe, Kapitelwiedergabe und einige zusätzliche Ereignisse ab.

## VHL-Codevergleich: INITIALISIERUNG

### Objektinitialisierung

| 1.x API | 2.x API |
| --- | --- |
| `Heartbeat()` | `MediaHeartbeat()` |
| `VideoPlayerPlugin()` | `MediaHeartbeatConfig()` |
| `AdobeAnalyticsPlugin()` |  |
| `HeartbeatPlugin()` |  |

#### Initialisierung des Videoplayer-Plugins (1.x) {#plugin-init-1.x}

```js
this._playerPlugin = new VideoPlayerPlugin( new SampleVideoPlayerPluginDelegate(this._player));
var playerPluginConfig = new VideoPlayerPluginConfig();
playerPluginConfig.debugLogging = true;

// Set up the AppMeasurement plugin 
this._aaPlugin = new AdobeAnalyticsPlugin( appMeasurement, new SampleAdobeAnalyticsPluginDelegate());
var aaPluginConfig = new AdobeAnalyticsPluginConfig();
aaPluginConfig.channel = Configuration.HEARTBEAT.CHANNEL;
aaPluginConfig.debuglogging = true;
this._aaPlugin.configure(aaPluginConfig);

// Set up the AdobeHeartbeat plugin 
var ahPlugin = new AdobeHeartbeatPlugin( new SampleAdobeHeartbeatPluginDelegate());
var ahPluginConfig = new AdobeHeartbeatPluginConfig( configuration.HEARTBEAT.TRACKING_SERVER, configuration.HEARTBEAT.PUBLISHER);
ahPluginConfig.ovp = configuration.HEARTBEAT.OVP;
ahPluginConfig.sdk = configuration.HEARTBEAT.SDK;
ahPluginConfig.debugLogging = true;
ahPlugin.configure(ahPluginConfig);
var plugins = [this._playerPlugin, this._aaPlugin, ahPlugin];

// Set up and configure the heartbeat library this._heartbeat = new Heartbeat(new SampleHeartbeatDelegate(), plugins);
var configData = new HeartbeatConfig();
configData.debugLogging = true;
this._heartbeat.configure(configData);
```

#### Media Heartbeat-Initialisierung (2.x) {#mh-init-2.x}

```js
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
mediaConfig.playerName = Configuration.PLAYER.NAME;
mediaConfig.debugLogging = true;
mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
mediaConfig.ssl = false;
mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
this._mediaHeartbeat = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

### Delegates

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPluginDelegate()` | `MediaHeartbeatDelegate()` |
| `VideoPlayerPluginDelegate().getVideoInfo` | `MediaHeartbeatDelegate().getCurrentPlaybackTime` |
| `VideoPlayerPluginDelegate().getAdBreakInfo` | `MediaHeartbeatDelegate().getQoSObject` |
| `VideoPlayerPluginDelegate().getAdInfo` |  |
| `VideoPlayerPluginDelegate().getChapterInfo` |  |
| `VideoPlayerPluginDelegate().getQoSInfo` |  |
| `VideoPlayerPluginDelegate().get.onError` |  |
| `AdobeAnalyticsPluginDelegate()` |  |

#### VideoPlayerPluginDelegate (1.x) {#player-plugin-delegate-1.x}

```js
$.extend(SampleVideoPlayerPluginDelegate.prototype, VideoPlayerPluginDelegate.prototype);

function SampleVideoPlayerPluginDelegate(player) { 
    this._player = player;
} 

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = function() { 
    return this._player.getAdBreakInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = function() { 
    return this._player.getQoSInfo();
};
```

#### AdobeAnalyticsPluginDelegate (1.x) {#analytics-plugin-delegate-1.x}

```js
$.extend(SampleAdobeAnalyticsPluginDelegate.prototype, AdobeAnalyticsPluginDelegate.prototype);

function SampleAdobeAnalyticsPluginDelegate() {} 

SampleAdobeAnalyticsPluginDelegate.prototype.onError = function(errorInfo) { 
    console.log("AdobeAnalyticsPlugin error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### HeartbeatDelegate (1.x) {#hb-delegate-1.x}

```js
$.extend(SampleHeartbeatDelegate.prototype, HeartbeatDelegate.prototype);

function SampleHeartbeatDelegate() {} 

SampleHeartbeatDelegate.prototype.onError = function(errorInfo) { 
    console.log("Heartbeat error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### MediaHeartbeatDelegate (2.x) {#mh-delegate-2.x}

```js
ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, MediaHeartbeatDelegate.prototype);

function SampleMediaHeartbeatDelegate(player) { 
    this._player = player;
} 

SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() { 
    return this._player.getCurrentPlaybackTime();
};

SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() { 
    return this._player.getQoSInfo();
};

this._mediaHeartbeat = new MediaHeartbeat(new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

## VHL-Codevergleich: CORE-WIEDERGABE

### Sitzungsstart

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.trackVideoLoad()` | `MediaHeartbeat.createMediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |

#### Sitzungsstart (1.x) {#session-start-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    this._playerPlugin.trackVideoLoad();
};

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Sitzungsstart (2.x) {#session-start-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

### Standard-Videometadaten

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Standard-Metadaten (1.x) {#std-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');

    var contextData = {};

    // Setting Standard Video Metadata 
    contextData[VideoMetadataKeys.SEASON] = "sample season";
    contextData[VideoMetadataKeys.SHOW] = "sample show";
    contextData[VideoMetadataKeys.EPISODE] = "sample episode";
    contextData[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    contextData[VideoMetadataKeys.GENRE] = "sample genre";
    contextData[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc. 
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Standard-Metadaten (2.x) {#std-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);

    // Set standard Video Metadata 
    var standardVideoMetadata = {};
    standardVideoMetadata[VideoMetadataKeys.SEASON] = "sample season";
    standardVideoMetadata[VideoMetadataKeys.SHOW] = "sample show";
    standardVideoMetadata[VideoMetadataKeys.EPISODE] = "sample episode";
    standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    standardVideoMetadata[VideoMetadataKeys.GENRE] = "sample genre";
    standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";
    
    // Etc. 
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Anstatt die Standard-Video-Metadaten über die `AdobeAnalyticsPlugin.setVideoMetadata()`-API festzulegen, werden diese in VHL 2.0 über den MediaObject-Schlüssel `MediaObject.MediaObjectKey.StandardVideoMetadata()` festgelegt.

### Anwenderspezifische Video-Metadaten

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Benutzerdefinierte Metadaten (1.x) {#custom-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Benutzerdefinierte Metadaten (2.x) {#custom-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Hinweis: Anstatt die benutzerspezifischen Video-Metadaten über die `AdobeAnalyticsPlugin.setVideoMetadata()`-API festzulegen, werden die Video-Metadaten in VHL 2.0 über die `MediaHeartbeat.trackSessionStart()`-API festgelegt.


### Wiedergabe

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackPlay()` | `MediaHeartbeat.trackPlay()` |

#### Wiedergabe (1.x) {#playback-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._playerPlugin.trackSeekStart();
};
```

#### Wiedergabe (2.x) {#playback-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};
```

### Anhalten

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackPause()` | `MediaHeartbeat.trackPausel()` |

#### Anhalten (1.x) {#pause-1.x}

```js
VideoAnalyticsProvider.prototype._onPause = function() { 
    console.log('Player event:X PAUSE');
    this._playerPlugin.trackPause();
};
```

#### Anhalten (2.x) {#pause-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Abschluss der Suche

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackSeekComplete()` | `MediaHeartbeat.`<br/>  `trackEvent(MediaHeartbeat.Event.SeekComplete)` |

#### Suchen (1.x) {#seek-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._playerPlugin.trackSeekComplete();
};
```

#### Suchen (2.x) {#seek-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};
```

### Pufferstart

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackBufferStart()` | `MediaHeartbeat.trackEvent(`<br/>  `MediaHeartbeat.Event.BufferStart)` |

#### Start der Pufferung (1.x) {#buffer-start-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._playerPlugin.trackBufferStart();
};
```

#### Start der Pufferung (2.x) {#buffer-start-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};
```

### Buffer Complete

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackBufferComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BufferComplete)` |

#### Abschluss der Pufferung (1.x) {#buffer-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._playerPlugin.trackBufferComplete();
};
```

#### Abschluss der Pufferung (2.x) {#buffer-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Abschluss der Wiedergabe

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackComplete()` | `MediaHeartbeat.trackComplete()` |

#### Abschluss der Wiedergabe (1.x) {#playback-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._playerPlugin.trackComplete(function() { 
        console.log( "The completion of the content has been tracked.");
    });
};
```

#### Abschluss der Wiedergabe (2.x) {#playback-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._mediaHeartbeat.trackComplete();
};
```

## VHL-Codevergleich: ANZEIGENWIEDERGABE

### Werbung gestartet

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdStart()` | `MediaHeartbeat.createAdBreakObject()` |
| `VideoPlayerPluginDelegate.getAdBreakInfo()` | `MediaHeartbeat.createAdObject()` |
| `VideoPlayerPluginDelegate.getAdInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakStart)` |
|  | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdStart)` |

#### Start der Anzeige (1.x) {#ad-start-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    this._playerPlugin.trackAdStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo(); 
};
```

#### Start der Anzeige (2.x) {#ad-start-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = {};

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

### Standard-Anzeigenmetadaten

| 1.x-API | 2.x-API |
| --- | --- |
| `AdMetadataKeys()` | `MediaHeartbeat.createAdObject()` |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.trackAdStart()` |

#### Standard-Anzeigenmetadaten (1.x) {#ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Standard-Anzeigenmetadaten (2.x) {#ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);

    // Set standard Ad Metadata 
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Anstatt die Standard-Anzeigenmetadaten über die `AdobeAnalyticsPlugin.setVideoMetadata()`-API einzustellen, werden diese in VHL 2.0 über den `AdMetadata`-Schlüssel `MediaObject.MediaObjectKey.StandardVideoMetadata` festgelegt.

### Anwenderspezifische Anzeigenmetadaten

| 1.x-API | 2.x-API |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
|  | `MediaHeartbeat.trackAdStart()` |

#### Benutzerdefinierte Anzeigenmetadaten (1.x) {#custom-ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var contextData = {};

    // Setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Benutzerdefinierte Anzeigenmetadaten (2.x) {#custom-ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { 
        affiliate: "Sample affiliate", 
        campaign: "Sample ad campaign" 
    };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Anstatt die benutzerdefinierten Anzeigenmetadaten über die `AdobeAnalyticsPlugin.setVideoMetadata`-API festzulegen, werden die Standard-Anzeigenmetadaten in VHL 2.0 über die `MediaHeartbeat.trackAdStart()`-API festgelegt.

### Ad Skip

| 1.x-API | 2.x-API |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
|  | `MediaHeartbeat.trackAdStart()` |

#### Überspringen einer Anzeige (1.x) {#ad-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};
```

#### Überspringen einer Anzeige (2.x) {#ad-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onAdSkip = function() { 
    console.log('Player event: AD_SKIP');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};
```

>[!NOTE]
>In VHL-1.5.X-APIs müssen `getAdinfo()` und `getAdBreakInfo()` null zurückgeben, wenn sich die Abspielposition im Player außerhalb der Werbeunterbrechung befindet.

### Werbung beendet

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackAdComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdComplete)` |
|  | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakComplete)` |

#### Abschluss der Anzeige (1.x) {#ad-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._playerPlugin.trackAdComplete();
};
```

#### Abschluss der Anzeige (2.x) {#ad-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

## VHL-Codevergleich: KAPITELWIEDERGABE

### Chapter Start

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.createChapterObject` |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Kapitelstart (1.x) {#chap-start-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._playerPlugin.trackChapterStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

#### Kapitelstart (2.x) {#chap-start-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Übersprungenes Kapitel

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterSkip)` |

#### Überspringen eines Kapitels (1.x) {#chap-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

>[!NOTE]
>In VHL-1.5.X-APIs muss `getChapterinfo()` null zurückgeben, wenn sich die Abspielposition im Player außerhalb der Kapitelgrenzen befindet.

#### Überspringen eines Kapitels (2.x) {#chap-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterSkip = function() { 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

### Anwenderspezifische Kapitelmetadaten

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.createChapterObject()` |
| `AdobeAnalyticsPlugin.setChapterMetadata()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Benutzerdefinierte Kapitelmetadaten (1.x) {#chap-cust-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._aaPlugin.setChapterMetadata({ 
        segmentType: "Sample segment type" 
    });
    this._playerPlugin.trackChapterStart();
};
```

#### Benutzerdefinierte Kapitelmetadaten (2.x) {#chap-cust-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { 
        segmentType: "Sample segment type" 
    };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Kapitelbeendigung

| 1.x-API | 2.x-API |
| --- | --- |
| `trackChapterComplete()` | `trackEvent(MediaHeartbeat.Event.ChapterComplete)` |

#### Kapitelbeendigung (1.x) {#chap-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._playerPlugin.trackChapterComplete();
};
```

#### Kapitelbeendigung (2.x) {#chap-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};
```

## VHL-Codevergleich: ANDERE EREIGNISSE

### Bitratenänderung

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBitrateChange()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BitrateChange)` |

#### Bitratenänderung (1.x) {#bitrate-chg-1.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosInfo to return the updated bitrate 
    this._playerPlugin.trackBitrateChange();
};
```

#### Bitratenänderung (2.x) {#bitrate-chg-2.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosObject to return the updated bitrate 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange);
};
```

### Wiederaufnahme des Videos

| 1.x-API | 2.x-API |
| --- | --- |
| `VideoInfo.resumed()` | `MediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |
| `VideoPlayerPlugin.trackVideoLoad()` |  |

#### Wiederaufnahme des Videos (1.x) {#video-resume-1.x}

```js
this._videoInfo.resumed=true;
```

```js
VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Wiederaufnahme des Videos (2.x) {#video-resume-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.playerName, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

Weitere Informationen zum Tracking von Videos mit 2.x finden Sie unter [Tracking von Kernvideowiedergabe](/help/sdk-implement/track-av-playback/track-core-overview.md).
