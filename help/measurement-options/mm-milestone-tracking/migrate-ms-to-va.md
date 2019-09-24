---
seo-title: Migration von Milestone zu Media Analytics
title: Migration von Milestone zu Media Analytics
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Migration von Milestone zu Media Analytics {#migrating-from-milestone-to-media-analytics}

## Überblick {#section_ihl_nbz_cfb}

Die grundlegenden Prinzipien der Videomessung sind bei Milestone und Media Analytics gleich: Es werden Videoplayer-Ereignisse aufgenommen und auf Analysemethoden übertragen, während gleichzeitig Playermetadaten und -werte erfasst und auf Analysevariablen übertragen werden. Die Media Analytics-Lösung ist aus Milestone hervorgegangen, sodass viele der Methoden und Kennzahlen gleich sind, aber der Konfigurationsansatz und der Code haben sich stark verändert. Es sollte möglich sein, den Player-Ereigniscode zu aktualisieren, um auf die neuen Methoden von Media Analytics zu verweisen. Weitere Informationen zur Implementierung von Media Analytics finden Sie unter [SDK-Übersicht](/help/sdk-implement/setup/setup-overview.md) und [Verfolgungsübersicht](/help/sdk-implement/track-av-playback/track-core-overview.md) .

Die folgenden Tabellen enthalten Übersetzungen zwischen der Milestone- und der Media Analytics-Lösung.

## Migrationsleitfaden {#section_iyb_pbz_cfb}

### Variablenreferenz

| Milestone-Metrik | Variablentyp | Media Analytics-Metrik |
| --- | --- | --- |
| Inhalt | Ablauf<br/><br/>von eVarDefault: Besuch | Inhalt |
| Content-Typ | eVar<br/><br/> Default expiration: Page view | Content-Typ |
| Inhaltsbesuchszeit | Ereignis-<br/><br/> Typ: Zähler | Inhaltsbesuchszeit |
| Videoaufrufe | Ereignis-<br/><br/> Typ: Zähler | Videoaufrufe |
| Videobeendigungen | Ereignis-<br/><br/> Typ: Zähler | Inhaltsbeendigung |

### Medienmodulvariablen

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone-Syntax
</th>
<th>Media Analytics
</th>
<th>Media Analytics-Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Alle Media Analytics-Daten werden nur über Kontextdaten gesendet.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segment View":"event2", "a.media.complete":"event7", "a.media.milestones": { 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>nicht angegeben
</td>
<td>Media Analytics-Kontextdaten werden automatisch in reservierte Variablen eingetragen. Zuordnung zu eVars, Requisiten und Ereignissen ist innerhalb des Implementierungscodes nicht mehr erforderlich. Kunden können Kontextdaten über Verarbeitungsregeln auf Variablen abbilden.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>nicht angegeben
</td>
<td>Nicht mehr benötigt, da die Zuordnung über reservierte Variablen und Verarbeitungsregeln erfolgt.
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>nicht angegeben
</td>
<td>Nicht mehr benötigt, da die Zuordnung über reservierte Variablen und Verarbeitungsregeln erfolgt.
</td>
</tr>
</tbody>
</table>

### Optionale Variablen

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone-Syntax
</th>
<th>Media Analytics
</th>
<th>Media Analytics-Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Wir bieten keine vorkonfigurierten Playerzuordnungen mehr an.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams = true
</pre>
</td>
<td>nicht angegeben
</td>
<td>Wir bieten keine vorkonfigurierten Playerzuordnungen mehr an.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset = true
</pre>
</td>
<td>nicht angegeben
</td>
<td>Content Complete unterstützt nur eine 100 %-Fortschrittsmarkierung.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold = 1
</pre>
</td>
<td>nicht angegeben
</td>
<td>Content Complete unterstützt nur eine 100 %-Fortschrittsmarkierung.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Custom Player Name"
</pre>
</td>
<td>
SDK-Schlüssel: playerName; 
API-Schlüssel: media.playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds = 15
</pre>
</td>
<td>nicht angegeben
</td>
<td>Media Analytics ist auf 10 Sekunden für Inhalte und 1 Sekunde für Anzeigen eingestellt. Es sind keine weiteren Optionen verfügbar.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestones = "25,50,75";
</pre>
</td>
<td>nicht angegeben
</td>
<td>Media Analytics verfolgt die Fortschrittsmarkierungen immer bei 10, 25, 50, 75 und 95 %.
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>nicht angegeben
</td>
<td>Media Analytics verfolgt die Fortschrittsmarkierungen immer bei 10, 25, 50, 75 und 95 %.
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Automatisches Tracking ist nicht mehr verfügbar.
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Automatisches Tracking ist nicht mehr verfügbar.
</td>
</tr>
</tbody>
</table>

### Anzeigenverfolgungsvariablen

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone-Syntax
</th>
<th>Media Analytics
</th>
<th>Media Analytics-Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds = 15
</pre>
</td>
<td>nicht angegeben
</td>
<td>Media Analytics ist auf 10 Sekunden für Inhalte und 1 Sekunde für Anzeigen eingestellt. Es sind keine weiteren Optionen verfügbar.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestones = "25,50,75";
</pre>
</td>
<td>nicht angegeben
</td>
<td>Fortschrittsmarkierungen werden standardmäßig nicht für Anzeigen angeboten. Verwenden Sie berechnete Metriken, um Anzeigenfortschrittsmarken zu erstellen.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>nicht angegeben
</td>
<td>Media Analytics ist für Anzeigen auf 1 Sekunde eingestellt. Es sind keine weiteren Optionen verfügbar.
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Automatisches Tracking ist nicht mehr verfügbar.
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Automatisches Tracking ist nicht mehr verfügbar.
</td>
</tr>
</tbody>
</table>

### Medienmodulmethoden

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone-Syntax
</th>
<th>Media Analytics
</th>
<th>Media Analytics-Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart( mediaObject, contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName - (Erforderlich) Der Name des Videos, wie er in Videoberichten angezeigt werden soll.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject( name, mediaId, length, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength - (Erforderlich) Die Länge des Videos in Sekunden.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject( name, mediaId, length, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName - (Erforderlich) Der Name des Medienplayers, der zum Anzeigen des Videos verwendet wird, wie er in Videoberichten angezeigt werden soll.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent( MediaHeartbeat.
    Ereignis.
    AdBreakStart, adBreakObject); ...
trackEvent( MediaHeartbeat.
    Ereignis.
    AdStart, adObject, adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (Erforderlich) Der Name oder die ID der Anzeige.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject( name, adId, position, length)
</pre>
</td>
</tr>
<tr>
<td>
length(Erforderlich) Die Länge der Anzeige.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject( name, adId, position, length)
</pre>
</td>
</tr>
<tr>
<td>
playerName - (Erforderlich) Der Name der Medienlayer, die zum Anzeigen der Anzeige verwendet wird.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName - Name oder ID des primären Inhalts, in den die Anzeige eingebettet ist.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>nicht angegeben
</td>
<td>Automatisch vererbt
</td>
</tr>
<tr>
<td>
parentPod - Die Position im Hauptinhalt, an der die Anzeige wiedergegeben wurde.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject( name, position, startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition: Die Position in der Werbeunterbrechung, an der die Anzeige wiedergegeben wird.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject( name, adId, position, length)
</pre>
</td>
</tr>
<tr>
<td>
CPMTder CPM oder verschlüsselter CPM (mit "~" als Präfix), der für diese Wiedergabe gilt.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>nicht angegeben
</td>
<td>In Media Analytics nicht standardmäßig verfügbar
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>nicht angegeben
</td>
<td>Verwenden Sie einen Custom Link-Analyseaufruf zum Tracking von Klicks.
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> oder 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
oder
<pre>
trackEvent( MediaHeartbeat.
  Ereignis.
  SeekStart)
</pre> oder
<pre>
trackEvent( MediaHeartbeat.
  Ereignis.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Verwenden Sie anwenderdefinierte oder standardmäßige Metadaten, um zusätzliche Variablen festzulegen.
</td>
<td>
<pre>
var customVideoMetadata = { isUserLoggedIn: 
    "false", tvStation: 
    "Sample TV station", Programmierer: 
    "Beispielprogrammierer"}; ...
var standardVideoMetadata = {};
standardVideoMetadata [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = "Beispielauftritt";
standardVideoMetadata [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Beispielanzeige"; ...
mediaObject.setValue( MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>nicht angegeben
</td>
<td>Die Frequenz des Tracking-Aufrufs wird automatisch eingestellt.
</td>
</tr>
</tbody>
</table>

