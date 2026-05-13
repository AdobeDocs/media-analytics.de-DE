---
title: Details zum Testaufruf
description: Erfahren Sie, welche Anrufe Sie zur Validierung Ihrer Implementierung ausführen müssen.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/98Oa98xntOkB9Fe3NQ30FUdvVk0JNKJMyzjgSTvncdI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 616
ht-degree: 80%

---

# Details zum Testaufruf{#test-call-details}

## Medienplayer starten {#start-the-media-player}

### Start-Aufruf für Adobe Analytics (AppMeasurement) {#aa-start-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**wahr**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Anwenderspezifische Metadatenfelder**_ |
| _**`a.media.[value]`**_ | _**Standardmäßige Metadatenfelder**_ |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe Metadatendetails unten.
* Die Länge für lineare Streams sollte auf die beste Schätzung für die aktuelle Show eingestellt werden.

### Start-Aufruf für Standard-Metadaten in Adobe Analytics (AppMeasurement) {#std-metadata-aa}

| Parameter |  Wert (Beispiel)  |
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

### Start-Aufruf für benutzerdefinierte Metadaten in Adobe Analytics (AppMeasurement) {#custom-metadata-aa}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Start-Aufruf für Media Analytics (Heartbeats) {#ma-start-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Anwenderspezifische Metadatenfelder**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standardmäßige Metadatenfelder**_ |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe Metadatendetails unten.
* Die Abspielposition für lineare Streams beim Videostart sollte auf die seit Beginn der aktuellen Sendung verstrichenen Sekunden gesetzt werden, nicht auf 0.

### Start-Aufruf für Standard-Metadaten in Media Analytics (Heartbeats) {#std-metadata-ma}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `s:meta:a.media.show` | Serie |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Start-Aufruf für benutzerdefinierte Metadaten in Media Analytics (Heartbeats) {#custom-metadata-ma}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Start-Aufruf für Adobe Analytics in Media Analytics (Heartbeats) {#ma-aa-start}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Hinweise:**

* Dieser Aufruf gibt an, dass das Media SDK angefordert hat, in Adobe Analytics einen `pev2=ms_s`-Aufruf an den Adobe Analytics (AppMeasurement)-Server zu senden.
* Dieser Aufruf enthält keine anwenderdefinierten Metadaten.

## Werbung wiedergeben {#view-ad-playback}

### Anzeigenstart-Aufruf für Adobe Analytics (AppMeasurement) {#aa-ad-start-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**Metadatenfelder**_ |
| _**`a.media.[value]`**_ | _**Standardmäßige Metadatenfelder**_ |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe Metadatendetails unten.
* Die Anzeigenlänge kann auf -1 gesetzt werden, wenn sie beim Anzeigenstart nicht verfügbar ist.

### Anzeigenstart-Aufruf für Standard-Metadaten in Adobe Analytics (AppMeasurement) {#std-metadata-aa-ad-start}

| Parameter |  Wert (Beispiel)  |
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

### Anzeigenstart-Aufruf für benutzerdefinierte Metadaten in Adobe Analytics (AppMeasurement) {#custom-metadata-aa-ad-start}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Anzeigenstart-Aufruf für Media Analytics (Heartbeats) {#ma-ad-start-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Anwenderspezifische Metadatenfelder**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standardmäßige Metadatenfelder**_ |

**Hinweise:**

* Zusätzliche Kontextdatenvariablen sollten vorhanden sein und Metadaten enthalten. Siehe Metadatendetails unten.
* Die Anzeigenlänge kann auf -1 gesetzt werden, wenn sie beim Anzeigenstart nicht verfügbar ist.

### Anzeigenstart-Aufruf für Standard-Metadaten in Media Analytics (Heartbeats) {#std-metadata-ma-ad-start}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `s:meta:a.media.show` | Serie |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Anzeigenstart-Aufruf für benutzerdefinierte Metadaten im Media Analytics (Heartbeats) {#custom-metadata-ma-ad-start}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Anzeigenstart-Aufruf für Adobe Analytics in Media Analytics (Heartbeats) {#ma-aa-ad-start-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Anzeigenabspielaufruf für Media Analytics (Heartbeats) {#ma-ad-play-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Anzeigepause-Aufruf für Media Analytics (Heartbeats) {#ma-ad-pause-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Anzeige abgeschlossen-Aufruf für Adobe Analytics in Media Analytics (Heartbeats) {#ma-aa-ad-complete-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Hauptinhalt abspielen {#play-main-content}

### Abspielaufruf für Media Analytics (Heartbeats) {#ma-play-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Hinweise:**

* Die Position der Abspielleiste sollte bei jedem Abspielaufruf um 10 erhöht werden.
* Der Wert `l:event:duration` zeigt die Anzahl der Millisekunden seit dem letzten Tracking-Aufruf und sollte bei jedem 10-Sekunden-Aufruf ungefähr gleich bleiben.

## Hauptinhalt anhalten {#pause-main-content}

### Pause-Aufruf für Media Analytics (Heartbeats) {#ma-pause-call}

| Parameter |  Wert (Beispiel)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
