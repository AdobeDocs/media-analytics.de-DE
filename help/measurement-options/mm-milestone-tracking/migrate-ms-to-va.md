---
title: Migration von Milestone zu Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 100%

---


# Migration von Milestone zu Media Analytics {#migrating-from-milestone-to-media-analytics}

## Überblick {#overview}

Die Hauptkonzepte der Videomessung sind bei Milestone und Media Analytics identisch. Dabei werden Videoplayer-Ereignisse verwendet und Analysemethoden zugeordnet. Außerdem werden Player-Metadaten und -Werte erfasst und Analytics-Variablen zugeordnet. Die Media Analytics-Lösung wurde aus Milestone entwickelt. Viele der Methoden und Metriken sind identisch. Konfigurationsansätze und Code wurden jedoch erheblich geändert. Es sollte möglich sein, den Player-Ereignis-Code so zu aktualisieren, dass er auf die neuen Media Analytics-Methoden verweist. Weitere Informationen zur Implementierung von Media Analytics finden Sie unter [SDK-Übersicht](/help/sdk-implement/setup/setup-overview.md) und [Tracking-Übersicht](/help/sdk-implement/track-av-playback/track-core-overview.md).

Die folgenden Tabellen enthalten Übersetzungen zwischen der Milestone- und der Media Analytics-Lösung.

## Migrationsleitfaden {#migration-guide}

### Variablenreferenz

| Milestone-Metrik | Variablentyp | Media Analytics-Metrik |
| --- | --- | --- |
| Inhalt | eVar <br/><br/>Standardgültigkeit: Besuch | Inhalt |
| Content-Typ | eVar<br/><br/> Standardgültigkeit: Seitenansicht | Content-Typ |
| Inhaltsbesuchszeit | Ereignistyp <br/><br/>: Zähler | Inhaltsbesuchszeit |
| Videoaufrufe | Ereignistyp <br/><br/>: Zähler | Videoaufrufe |
| Videobeendigungen | Ereignistyp <br/><br/>: Zähler | Inhaltsbeendigung |

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
<th>Syntax von Media Analytics
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
s.Media.trackUsingContextData
  = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Alle Medienanalysedaten werden nur mit Kontextdaten gesendet.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones": {
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
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
s.Media.trackVars = 
  "events,
  prop2,
  eVar1,
  eVar2,
  eVar3";
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
s.Media.trackEvents = 
  "event1,
  event2,
  event3,
  event4,
  event5,
  event6,
  event7"
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
<th>Syntax von Media Analytics
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
s.Media.autoTrack
  = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Wir bieten keine vordefinierten Player-Zuordnungen mehr an.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams
  = true
</pre>
</td>
<td>nicht angegeben
</td>
<td>Wir bieten keine vordefinierten Player-Zuordnungen mehr an.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset
  = true
</pre>
</td>
<td>nicht angegeben
</td>
<td>Inhaltsbeendigung unterstützt nur eine 100%ige Fortschrittsmarkierung.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold
  = 1
</pre>
</td>
<td>nicht angegeben
</td>
<td>Inhaltsbeendigung unterstützt nur eine 100%ige Fortschrittsmarkierung.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName
  = "Custom Player Name"
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
  trackSeconds
  = 15
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
  trackMilestones
  = "25,50,75";
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
  trackOffsetMilestones
  = "20,40,60";
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
s.Media.segmentByMilestones
  = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Das automatische Tracking ist nicht mehr verfügbar
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones
  = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Das automatische Tracking ist nicht mehr verfügbar
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
<th>Syntax von Media Analytics
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
  adTrackSeconds
  = 15
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
  adTrackMilestones
  = "25,50,75";
</pre>
</td>
<td>nicht angegeben
</td>
<td>Fortschrittsmarkierungen werden nicht standardmäßig für Anzeigen bereitgestellt. Verwenden Sie berechnete Metriken, um Anzeigenfortschrittsmarken zu erstellen.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones
  = "20,40,60";
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
  adSegmentByMilestones
  = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Das automatische Tracking ist nicht mehr verfügbar
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones
  = true;
</pre>
</td>
<td>nicht angegeben
</td>
<td>Das automatische Tracking ist nicht mehr verfügbar
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
<th>Syntax von Media Analytics
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
s.Media.open(
  mediaName,
  mediaLength,
  mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart(
  mediaObject, 
  contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName (erforderlich): Der Name des Videos, wie er in Videoberichten angezeigt werden soll.
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
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength (erforderlich): Die Länge des Videos in Sekunden.
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
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName (erforderlich): Der Name des Medienplayers, mit dem das Video wiedergegeben wird, wie er in Videoberichten angezeigt werden soll.
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
s.Media.openAd(
  name,
  length,
  playerName,
  parentName,
  parentPod,
  parentPodPosition,
  CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent(
  MediaHeartbeat.
    Ereignis.
    AdBreakStart, 
  adBreakObject);
...
trackEvent(
  MediaHeartbeat.
    Ereignis.
    AdStart, 
  adObject, 
  adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name (erforderlich): Name oder ID der Anzeige.
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
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
length (erforderlich): Länge der Anzeige.
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
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
playerName (erforderlich): Name des Medienplayers, mit dem die Anzeige wiedergegeben wird.
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
parentName: Name oder ID des Hauptinhalts, in den die Anzeige eingebettet ist.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>nicht angegeben
</td>
<td>Automatisch geerbt
</td>
</tr>
<tr>
<td>
parentPod: Die Position im Hauptinhalt, an der die Anzeige wiedergegeben wurde.
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
createAdBreakObject(
  name, 
  position, 
  startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition: Die Position in der Werbeunterbrechung, an der die Anzeige wiedergegeben wurde.
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
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
CPM: CPM oder verschlüsselter CPM (mit „~“ als Präfix) für diese Wiedergabe.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>nicht angegeben
</td>
<td>In Media Analytics nicht standardmäßig verfügbar.
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(
  name,
  offset)
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
s.Media.close(
  mediaName)
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
s.Media.complete(
  name,
  offset)
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
s.Media.play(
  name,
  offset,
  segmentNum,
  segment,
  segmentLength)
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
s.Media.stop(
  mediaName,
  mediaOffset)
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
trackEvent(
  MediaHeartbeat.
  Ereignis.
  SeekStart)
</pre> oder
<pre>
trackEvent(
  MediaHeartbeat.
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
var customVideoMetadata = 
{
  isUserLoggedIn: 
    "false",
  tvStation: 
    "Sample TV station",
  programmer: 
    "Sample programmer"
};
...
var standardVideoMetadata 
  = {};
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = 
  "Sample Episode";
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Sample Show";
...
mediaObject.setValue(
  MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, 
  standardVideoMetadata);
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
s.Media.track(
  mediaName)
</pre>
</td>
<td>nicht angegeben
</td>
<td>Die Tracking-Aufrufhäufigkeit wird automatisch festgelegt.
</td>
</tr>
</tbody>
</table>

