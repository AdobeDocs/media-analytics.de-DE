---
title: JavaScript 3.x Media SDK API-Referenz
description: API-Referenz für Media SDK JavaScript 3.x (Klassen ADB.Media und ADB.MediaConfig).
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# JavaScript 3.x Media SDK API-Referenz

>[!BEGINSHADEBOX]

Auf dieser Seite wird die reine Analytics-SDK JavaScript 3.x beschrieben. Die empfohlene Implementierung finden Sie unter [Implementieren von Streaming-Medien mit der Edge Network](/help/implementation/edge/edge-web-sdk.md).

>[!ENDSHADEBOX]

## ADB.media

### Statische Methoden

+++configure

Konfiguriert MediaSDK für das Tracking. Diese Methode sollte einmal aufgerufen werden, bevor Tracker-Instanzen auf einer Seite erstellt werden.

**Syntax**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| Variablenname | Typ | Beschreibung |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | Gültige Medienkonfiguration |
| `appMeasurement` | Objekt | AppMeasurement-Instanz |

**Beispiel**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

Erstellt eine Medieninstanz zum Tracking der Wiedergabesitzung. Gibt `null` zurück, wenn es vor dem Konfigurieren des Mediums aufgerufen wurde.

**Syntax**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| Variablenname | Typ | Erforderlich | Beschreibung |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | Tracker-Konfiguration | Nein | Tracker-Konfigurationsobjekt. |

**Beispiel**

```javascript
var tracker = ADB.Media.getInstance();
```

Um `channel` oder `playerName` pro Tracker-Instanz zu überschreiben, übergeben Sie die Überschreibungswerte im Tracker-Konfigurationsobjekt.

**Beispiel mit Tracker-Konfiguration**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

Erstellt ein -Objekt, das Medieninformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden.

**Syntax**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| Variablenname | Typ | Beschreibung |
| :--- | :--- | :--- |
| `name` | string | Nicht leere Zeichenfolge, die den Mediennamen angibt |
| `id` | string | Nicht leere Zeichenfolge, die eine eindeutige Medienkennung angibt |
| `length` | number | Positive Zahl, die die Länge des Mediums in Sekunden angibt. Verwenden Sie `0`, wenn die Länge unbekannt ist. |
| `streamType` | string | Stream-Typ oder nicht leere Zeichenfolge, um den Medien-Stream-Typ zu kennzeichnen. |
| `mediaType` | Medientyp | Typ des Mediums (Audio oder Video) |

**Beispiel**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

Erstellt ein -Objekt, das Adbreak-Informationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden.

**Syntax**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| Variablenname | Typ | Beschreibung |
| :--- | :--- | :--- |
| `name` | string | Nicht leere Zeichenfolge, die den AdBreak-Namen angibt (Pre-roll, Mid-roll und Post-roll) |
| `position` | number | Die Position der Anzeigenunterbrechung im Inhalt, beginnend mit 1 |
| `startTime` | number | Abspielpositionswert bei Start der Werbeunterbrechung. |

**Beispiel**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

Erstellt ein -Objekt, das Anzeigeninformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden.

**Syntax**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| Variablenname | Typ | Beschreibung |
| :--- | :--- | :--- |
| `name` | string | Nicht leere Zeichenfolge, die Anzeigenamen angibt |
| `id` | string | Nicht leere Zeichenfolge, die die Werbe-ID angibt |
| `position` | number | Die Positionsnummer der Anzeige innerhalb der Werbeunterbrechung, beginnend mit 1 |
| `length` | number | Positive Zahl für die Länge der Anzeige |

**Beispiel**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

Erstellt ein -Objekt, das Kapitelinformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden.

**Syntax**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| Variablenname | Typ | Beschreibung |
| :--- | :--- | :--- |
| `name` | string | Nicht leere Zeichenfolge, die den Kapitelnamen angibt |
| `position` | number | Die Position des Kapitels innerhalb des Inhalts, beginnend mit 1 |
| `length` | number | Positive Zahl, die die Länge des Kapitels angibt |
| `startTime` | number | Abspielkopfwert am Anfang des Kapitels |

**Beispiel**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

Erstellt ein -Objekt, das Statusinformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden.

**Syntax**

```javascript
ADB.Media.createStateObject(name)
```

| Variablenname | Typ | Beschreibung |
| :--- | :--- | :--- |
| `name` | string | Player-Status oder nicht leere Zeichenfolge, die den Statusnamen angibt |

**Beispiel**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

Erstellt ein -Objekt, das QoE-Informationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden.

**Syntax**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| Variablenname | Typ | Beschreibung |
| :--- | :--- | :--- |
| `bitrate` | number | Positive Zahl, die die aktuelle Bitrate angibt (0, wenn unbekannt) |
| `startupTime` | number | Positive Zahl, die die Startzeit angibt (0, wenn unbekannt) |
| `fps` | number | Positive Zahl für aktuelle fps (0, wenn unbekannt) |
| `droppedFrames` | number | Positive Zahl, die die Anzahl der ausgelassenen Frames angibt (0, falls unbekannt) |

**Beispiel**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

Gibt die MediaSDK-Version zurück.

**Syntax**

```javascript
ADB.Media.version
```

**Beispiel**

```javascript
console.log(ADB.Media.version);
```

+++

### Instanzmethoden

+++trackSessionStart

Verfolgen Sie die Absicht, die Wiedergabe zu starten. Dadurch wird eine Tracking-Sitzung auf der Media Tracker-Instanz gestartet. Siehe auch Medien-Wiederaufnahme .

**Syntax**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| Variablenname | Beschreibung | erforderlich |
| :--- | :--- | :---: |
| `mediaObject` | Medieninformationen, die mithilfe der `createMediaObject`-Methode erstellt wurden. | Ja |
| `contextData` | Optionale Medien-Kontextdaten. Verwenden Sie für Standard-Metadatenschlüssel Standardvideokonstanten oder Standardaudiokonstanten. | Nein |

**Beispiel**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

Tracking der Medienwiedergabe oder Wiederaufnahme nach einer vorherigen Pause.

**Syntax**

```javascript
ADB.Media.trackPlay();
```

**Beispiel**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

Verfolgen der Medienpause.

**Syntax**

```javascript
ADB.Media.trackPause();
```

**Beispiel**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

Verfolgen Sie den Abschluss von Medien. Rufen Sie diese Methode nur auf, wenn die Medien vollständig angezeigt wurden.

**Syntax**

```javascript
ADB.Media.trackComplete();
```

**Beispiel**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

Verfolgen Sie das Ende einer Anzeigesitzung. Rufen Sie diese Methode auch dann auf, wenn der Benutzer das Medium nicht bis zum Abschluss anzeigt.

**Syntax**

```javascript
ADB.Media.trackSessionEnd();
```

**Beispiel**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

Tracking eines Fehlers bei der Medienwiedergabe.

**Syntax**

```javascript
ADB.Media.trackError(errorId);
```

| Variablenname | Beschreibung | erforderlich |
| :--- | :--- | :---: |
| `errorId` | Nicht leere Zeichenfolge mit Fehlerinformationen | Ja |

**Beispiel**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

Methode zum Tracking von Medienereignissen.

| Variablenname | Beschreibung |
| :--- | :--- |
| `event` | Medienereignis |
| `info` | Für `AdBreakStart` Ereignis werden die AdBreak-Informationen mithilfe der `createAdBreakObject`-Methode erstellt. Für `AdStart` Ereignis werden die Anzeigeninformationen mithilfe der `createAdObject`-Methode erstellt. Für `ChapterStart` Ereignis werden die Kapitelinformationen mithilfe der `createChapterObject`-Methode erstellt. Bei `StateStart`- und `StateEnd`-Ereignissen werden die Statusinformationen mithilfe der `createStateObject`-Methode erstellt. Dies ist für andere Ereignisse nicht erforderlich. |
| `contextData` | Für `AdStart` und `ChapterStart` Ereignisse können optionale Kontextdaten bereitgestellt werden. Dies ist für andere Ereignisse nicht erforderlich. |

**Syntax**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**Beispiele**

**Tracking von Werbeunterbrechungen**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**Tracking von Anzeigen**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**Tracking-Kapitel**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**Status verfolgen**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**Tracking von Wiedergabeereignissen**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**Verfolgen von Bitratenänderungen**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

Stellen Sie dem Medien-Tracker den aktuellen Medien-Abspielkopf bereit. Rufen Sie für genaues Tracking diese Methode auf, wenn sich der Abspielkopf während der Wiedergabe ändert.

**Syntax**

```javascript
ADB.Media.updatePlayhead(time);
```

| Variablenname | Beschreibung |
| :--- | :--- |
| `time` | Aktueller Abspielkopf in Sekunden. Bei Video-on-demand (VOD) wird der Wert in Sekunden ab Beginn des Medienelements angegeben. Wenn der Player beim Live-Streaming keine Informationen zur Inhaltsdauer bereitstellt, kann der Wert als Anzahl der Sekunden seit Mitternacht (UTC) des Tages angegeben werden. Hinweis: Bei Verwendung von Fortschrittsmarken ist die Inhaltsdauer erforderlich und der Abspielkopf muss als Anzahl von Sekunden ab Beginn des Medienelements aktualisiert werden, beginnend mit 0. |

**Beispiel**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

Stellt dem Medien-Tracker aktuelle QoE-Informationen bereit. Rufen Sie diese Methode zur präzisen Nachverfolgung mehrmals auf, wenn der Media Player die aktualisierten QoE-Informationen bereitstellt.

**Syntax**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| Variablenname | Beschreibung |
| :--- | :--- |
| `qoeObject` | Aktuelle QoE-Informationen, die mithilfe der `createQoEObject`-Methode erstellt wurden. |

**Beispiel**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++vernichten

Zerstört die Tracker-Instanz.

**Syntax**

```javascript
ADB.Media.destroy();
```

**Beispiel**

```javascript
tracker.destroy();
```

+++

### Konstanten

+++Tracker-Konfiguration

Definiert die Konfigurationsschlüssel, die pro Tracker-Instanz festgelegt werden können.

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++Medientyp

Definiert den Typ eines aktuell verfolgten Mediums.

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++Stream-Typ

Definiert den Stream-Typ des aktuell verfolgten Inhalts.

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++Standard-Metadatenschlüssel

`ADB.Media.VideoMetadataKeys`, `ADB.Media.AudioMetadataKeys` und `ADB.Media.AdMetadataKeys` stellen die Kontextdatenschlüsselzeichenfolgen für Standardmetadaten bereit. Eine vollständige Liste der Schlüssel und der zugehörigen Berichtsvariablen finden Sie unter [Standard-Metadatenvariablenreferenz](/help/implementation/variables/standard-metadata/show.md).

+++

+++Medienereignisse

Definiert den Typ eines Tracking-Ereignisses.

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++Player-Status

Definiert Standardwerte zum Tracking des Player-Status.

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++Medienwiederaufnahme

Konstante, die angibt, dass die aktuelle Tracking-Sitzung eine zuvor geschlossene Sitzung wieder aufnimmt. Diese Informationen müssen beim Starten einer Tracking-Sitzung angegeben werden.

**Syntax**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**Beispiel**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| Schlüssel | Erforderlich | Beschreibung |
| :--- | :--- | :--- |
| `trackingServer` | Ja | Geben Sie den Namen des Mediensammlungs-API-Servers ein, an den die heruntergeladenen Medien-Tracking-Daten gesendet werden sollen. Wenden Sie sich an Ihren Adobe-Kundenbetreuer, um diese Informationen zu erhalten. |
| `channel` | Nein | Kanalnamen-Eigenschaft |
| `playerName` | Nein | Name des verwendeten Medien-Players |
| `appVersion` | Nein | Geben Sie die Version des Media Player-Programms/SDK ein |
| `debugLogging` | Nein | Aktiviert oder deaktiviert Media SDK-Protokolle (Standardwert: `false`) |
| `ssl` | Nein | Sendet Pings über SSL (Standardwert: `true`) |
