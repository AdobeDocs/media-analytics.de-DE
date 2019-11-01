---
title: Roku-Metadatenelemente
description: In diesem Thema werden die verfügbaren Roku-Metadatenschlüssel beschrieben.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Roku-Metadatenschlüssel{#roku-metadata-keys}

Standard-Metadaten für Video, Audio und Anzeige können für Medien- bzw. Anzeigeninfo-Objekte festgelegt werden. Geben Sie mithilfe der Konstantenschlüssel für Video-/Anzeigen-Metadaten das Wörterbuch an, das die Standardmetadaten zum Informationsobjekt enthält, bevor Sie die APIs verfolgen. Eine vollständige Liste der standardmäßigen Metadaten-Konstanten finden Sie unten in den Tabellen mit Beispielen.

## Video-Metadaten-Konstanten {#video-metadata-constants}

| Metadatenname | Kontextdatenschlüssel | Konstantenname |
| --- | --- | --- |
| Show | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Staffel | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episode | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Asset | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genre | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Erstes Sendedatum | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Datum der ersten digitalen Veröffentlichung | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Rating | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Urheber | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Netzwerk | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Sendungstyp | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Anzeigenladevorgang | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Autorisiert | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Tagesteil | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Stream-Format | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Audio-Metadatenkonstanten {#audio-metadata-constants}

| Metadatenname | Kontextdatenschlüssel | Konstantenname |
| --- | --- | --- |
| Künstler | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Beschriftung | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Autor | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Station | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Publisher | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Anzeigenmetadaten-Konstanten {#ad-metadata-constants}

| Metadatenname | Kontextdatenschlüssel | Konstantenname |
| --- | --- | --- |
| Advertiser | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| Kampagnen-ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| Creative-ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| Platzierungs-ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| Site-ID | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| Creative-URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Konstanten {#constants}

Sie können folgende Konstanten verwenden, um Medienereignisse zu verfolgen:

### Weitere Konstanten

| Konstante | Beschreibung   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Konstante bei Player als Fehlerquelle |

### MediaObjectkey-Konstanten (werden als Schlüssel in MediaObject-Instanzen verwendet)

| Konstante | Beschreibung   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Konstante zum Festlegen von Metadaten auf der `MediaInfo``trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Konstante zum Festlegen der Anzeigenmetadaten auf der `EventData``trackEvent` |
| `MEDIA_RESUMED` | Konstante für das Senden eines Heartbeats zur Videowiederaufnahme. To resume video tracking of previously stopped content, you need to set the `MEDIA_RESUMED` property on the `mediaInfo` object when you call `mediaTrackLoad`. (`MEDIA_RESUMED` is not an event that you can track using the `mediaTrackEvent` API.) `MEDIA_RESUMED` sollte auf true festgelegt werden, wenn die Anwendung das Tracking des Inhalts wiederaufnehmen möchte, nachdem ein Anwender die Wiedergabe angehalten hat und sie nun fortsetzen möchte. <br/><br/>Beispiel: Ein Anwender sieht sich 30 % des Inhalts an und schließt dann die App. Hierdurch wird die Sitzung beendet. Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they left off, then the application should set `MEDIA_RESUMED` to "true" while calling the `mediaTrackLoad` API. So lassen sich die beiden unterschiedlichen Mediensitzungen für denselben Videoinhalt verknüpfen. Im Folgenden finden Sie ein Implementierungsbeispiel: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>So erstellen Sie eine neue Sitzung für das Medium, jedoch sendet das SDK hierdurch auch eine Heartbeat-Anfrage mit dem Ereignistyp „resume“ (Fortsetzen), die in Berichten verwendet werden kann, um die beiden Mediensitzungen zu verknüpfen. |

### Content-Typ-Konstanten

| Konstante | Beschreibung   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Konstante für den Streamtyp „LIVE“ |
| `MEDIA_STREAM_TYPE_VOD` | Konstante für den Streamtyp „VOD“ |

### Ereignistyp-Konstanten (werden für den trackEvent-Aufruf verwendet)

| Konstante | Beschreibung   |
|---|---|
| `MEDIA_BUFFER_START` | Ereignistyp für den Start von Puffervorgängen |
| `MEDIA_BUFFER_COMPLETE` | Ereignistyp für den Abschluss von Puffervorgängen |
| `MEDIA_SEEK_START` | Ereignistyp für den Start von Suchvorgängen |
| `MEDIA_SEEK_COMPLETE` | Ereignistyp für den Abschluss von Suchvorgängen |
| `MEDIA_BITRATE_CHANGE` | Ereignistyp für Änderungen der Bitrate |
| `MEDIA_CHAPTER_START` | Ereignistyp für den Start eines Kapitels |
| `MEDIA_CHAPTER_COMPLETE` | Ereignistyp für den Abschluss eines Kapitels |
| `MEDIA_CHAPTER_SKIP` | Ereignistyp für den Start einer Anzeige |
| `MEDIA_AD_BREAK_START` | Ereignistyp für den Start einer Anzeige |
| `MEDIA_AD_BREAK_COMPLETE` | Ereignistyp für den Abschluss einer AdBreak |
| `MEDIA_AD_BREAK_SKIP` | Ereignistyp für das Überspringen einer AdBreak |
| `MEDIA_AD_START` | Ereignistyp für den Start einer Anzeige |
| `MEDIA_AD_COMPLETE` | Ereignistyp für den Abschluss einer Anzeige |
| `MEDIA_AD_SKIP` | Ereignistyp für das Überspringen einer Anzeige |

