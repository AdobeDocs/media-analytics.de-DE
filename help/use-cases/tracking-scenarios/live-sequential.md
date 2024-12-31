---
title: Live-Hauptinhalt mit sequentieller Verfolgung
description: Sehen Sie sich ein Beispiel für das Tracking von Live-Inhalten mit sequenzieller Verfolgung mithilfe des Media SDK an.
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
exl-id: 277a72b8-453b-41e5-b640-65c43587baf8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 98%

---

# Live-Hauptinhalt mit sequentieller Verfolgung{#live-main-content-with-sequential-tracking}

## Szenario {#scenario}

In diesem Szenario gibt es ein einziges Live-Asset ohne Anzeigen, das 40 Sekunden nach Eintritt eines Benutzers in den Live-Stream wiedergegeben wird.

Dieses Szenario ist mit dem Szenario [VOD-Wiedergabe ohne Anzeigen](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) identisch, allerdings wird hierbei ein Teil des Inhalts durchsucht und die Suche wird von einem Punkt im Hauptinhalt bis zu einem anderen Punkt durchgeführt.

| Auslöser | Heartbeat-Methode |  Netzwerkaufrufe  |  Hinweise   |
| --- | --- | --- | --- |
| Anwender klickt auf [!UICONTROL Abspielen] | trackSessionStart | Analytics Content Start, Heartbeat Content Start | Der Measurement Library ist nicht bekannt, dass es eine Pre-Roll-Anzeige gibt. Daher sind diese Netzwerkaufrufe mit dem Szenario [VOD-Wiedergabe ohne Anzeigen](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) identisch. |
| Das erste Bild des Inhalts wird wiedergegeben. | trackPlay | Heartbeat Content Play | Wenn Kapitelinhalte vor dem Hauptinhalt wiedergegeben werden, starten Heartbeats beim Beginn des Kapitels. |
| Inhalt wird wiedergegeben | | Content Heartbeats | Dieser Netzwerkaufruf ist mit dem Aufruf beim Szenario [VOD-Wiedergabe ohne Anzeigen](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) identisch. |
| Sitzung 1 beendet (Folge 1 beendet) | trackComplete / trackSessionEnd | Heartbeat Content Complete | „Complete“ bedeutet, dass Sitzung 1 für die erste Folge erreicht und vollständig angesehen wurde. Vor dem Start der Sitzung für die nächste Folge muss diese Sitzung beendet sein. |
| Episode2 gestartet (Session2 Start) | trackSessionStart | Inhaltsstart-Heartbeat-Inhaltsstart für Analytics | Dies tritt auf, wenn der Anwender die erste Folge geschaut und direkt mit einer weiteren Folge begonnen hat. |
| Erstes Medienbild | trackPlay | Heartbeat Content Play | Diese Methode löst den Timer aus. Ab diesem Zeitpunkt werden alle 10 Sekunden Heartbeats gesendet, solange die Wiedergabe läuft. |
| Inhalt wird wiedergegeben | | Content Heartbeats | |
| Sitzung beendet (Folge 2 beendet) | trackComplete / trackSessionEnd | Heartbeat Content Complete | „Complete“ bedeutet, dass Sitzung 2 für die zweite Folge erreicht und vollständig angesehen wurde. Vor dem Start der Sitzung für die nächste Folge muss diese Sitzung beendet sein. |

## Parameter {#parameters}

### Heartbeat Content Start

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:sc:rsid` | &lt;Adobe-Report Suite-ID> |  |
| `s:sc:tracking_serve` | &lt;Analytics-Tracking-Server-URL> |  |
| `s:user:mid` | `s:user:mid` | Sollte mit dem mid-Wert beim Adobe Analytics Content Start-Aufruf übereinstimmen |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Ihr Medienname> |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *optional* | Im Medium festgelegte benutzerdefinierte Metadaten |

## Heartbeat Content Play {#heartbeat-content-play}

Dies sollte fast genauso wie der Heartbeat Content Start-Aufruf aussehen, aber den Hauptunterschied im Parameter „s:event:type“ aufweisen. Alle Parameter sollten hier weiterhin vorhanden sein.

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Content Heartbeats {#content-heartbeats}

Während der Medienwiedergabe gibt es einen Timer, der alle 10 Sekunden einen oder mehrere Heartbeats für Hauptinhalte und jede Sekunde für Anzeigen sendet. Diese Heartbeats enthalten Informationen über Wiedergabe, Anzeigen, Pufferung und eine Reihe anderer Dinge. Der genaue Inhalt eines jeden Heartbeat geht über den Rahmen dieses Dokuments hinaus. Wichtig ist, dass Heartbeats laufend während der Wiedergabe ausgelöst werden.

Suchen Sie in den Content Heartbeats nach einigen spezifischen Elementen:

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;Position der Abspielleiste>, z. B. 50, 60, 70 | Dies sollte die aktuelle Position der Abspielleiste widerspiegeln. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Wenn die Wiedergabe für eine bestimmte Folge abgeschlossen ist (Abspielleiste überschreitet die Begrenzung für die Folge), wird ein „Heartbeat Content Complete“-Aufruf gesendet. Dies sieht wie andere Heartbeat-Aufrufe aus, enthält aber einige spezielle Dinge:

| Parameter | Wert | Hinweise |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Beispielcode {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

### Android

Die erwartete API-Aufrufreihenfolge lautet wie folgt:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., when there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing 1st episode/session.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2 /episode 2 of the same live stream.  
// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
//    start of session 2 
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue similarly tracking further sessions in the live stream if required 
```

### iOS

Die erwartete API-Aufrufreihenfolge lautet wie folgt:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
  
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
  
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing the first 
//    episode/session. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 4. Call trackSessionEnd to end session 1 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Start tracking session 2 / episode 2 of the same live stream, No need to  
// reinstantiate mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 5. Call trackSessionStart when the playhead reaches a point that denotes  
//    start of session 2 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 6. Call trackPlay to start tracking session 2 playback 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 7. Call trackComplete when the playback reaches the end of session 2,  
//    i.e., when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 
 
// 8. Call trackSessionEnd to end the session 2 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

### JavaScript

Die erwartete API-Aufrufreihenfolge lautet wie folgt:

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of a session,  
//    i.e., whn playback completes and finishes playing the 1st episode/session. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2/episode 2 of the same live stream. There is no need  
// to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
var mediaInfo2 = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

var mediaMetadata2 = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes  
//    the start of session 2 
this._mediaHeartbeat.trackSessionStart(mediaInfo2, mediaMetadata2); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```
