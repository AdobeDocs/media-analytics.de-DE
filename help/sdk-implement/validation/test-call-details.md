---
seo-title: Details zum Testaufruf
title: Details zum Testaufruf
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Details zum Testaufruf{#test-call-details}

## Videoplayer starten {#section_qts_xff_f2b}

### Media Analytics-Startanruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | wahr |
| `a.contentType` | vod |
| `custom.[value]` | Anwenderspezifische Metadatenfelder |
| `a.media.[value]` | Standardmäßige Metadatenfelder |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe unten zu Details für Metadaten.
* Die Länge für lineare Streams sollte auf die beste Schätzung für die aktuelle Sendung eingestellt werden.

### Standard-Metadaten in Media Analytics starten

| Parameter | Wert (Beispiel)   |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Heartbeat-Startaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | Anwenderspezifische Metadatenfelder |
| `s:meta:a.media.[value]` | Standardmäßige Metadatenfelder |

### Medienmetadaten in Media Analytics starten

| Parameter | Wert (Beispiel)   |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe unten zu Details für Metadaten.
* Die Position der Abspielleiste für lineare Streams sollte beim Videostart auf die Sekunden eingestellt werden, die seit Beginn der aktuellen Sendung verstrichen sind, nicht auf 0.

### Heartbeat Analytics-Startaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

### Medienmetadaten im Heartbeat-Startaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Standardmäßige Metadaten im Heartbeat-Startaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 04.07.2018 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

**Hinweise:**

* Dieser Aufruf zeigt an, dass die Heartbeat-Bibliothek angefordert hat, einen Analytics-pev2=ms_s-Aufruf an den Analyseserver zu senden.
* Dieser Aufruf enthält keine anwenderdefinierten Metadaten.

## Werbung wiedergeben {#section_wz3_yff_f2b}

### Media Analytics-Anzeigenstart-Aufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0,0 |
| `a.media.ad.view` | True |
| `custom.[value]` | Metadatenfelder |
| `a.media.[value]` | Standardmäßige Metadatenfelder |

**Hinweis:** Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe unten zu Details für Metadaten.

### Heartbeat-Anzeigenstartaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | Anwenderspezifische Metadatenfelder |
| `s:meta:a.media.[value]` | Standardmäßige Metadatenfelder |

### Medienmetadaten im Media Analytics-Anzeigenaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Standard-Metadaten im Media Analytics-Anzeigenstartaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe unten zu Details für Metadaten.
* Die Anzeigenlänge kann auf -1 gesetzt werden, wenn sie beim Anzeigenstart nicht verfügbar ist.

### Heartbeat Analytics-Anzeigenstartaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Medienmetadaten im Heartbeat Ad Start-Aufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Standardmäßige Metadaten im Heartbeat-Anzeigenstartaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 04.07.2018 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe unten zu Details für Metadaten.
* Die Anzeigenlänge kann auf -1 gesetzt werden, wenn sie beim Anzeigenstart nicht verfügbar ist.

### Heartbeat Anzeigenendeaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:event:type` | complete |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Heartbeat Anzeigenabspielaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

## Hauptinhalt abspielen {#section_u1l_1gf_f2b}

### Heartbeat Abspielaufruf

| Parameter | Wert (Beispiel)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Hinweise:**

* Die Position der Abspielleiste sollte bei jedem Abspielanruf um 10 erhöht werden.
* Der Wert `l:event:duration` zeigt die Anzahl der Millisekunden seit dem letzten Tracking-Aufruf und sollte bei jedem 10-Sekunden-Aufruf ungefähr gleich bleiben.

