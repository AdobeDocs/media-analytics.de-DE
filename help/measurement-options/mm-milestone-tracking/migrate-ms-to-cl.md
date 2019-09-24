---
seo-title: Migration von Milestone zu Custom Link
title: Migration von Milestone zu Custom Link
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Migration von Milestone zu Custom Link{#migrating-from-milestone-to-custom-link}

## Überblick {#section_xlc_fc2_dfb}

Die grundlegenden Prinzipien der Videomessung sind die gleichen wie beim Milestone- und Custom Link-Tracking, bei denen Videoplayer-Ereignisse aufgenommen und auf Analysemethoden übertragen werden, während gleichzeitig Playermetadaten und -werte erfasst und auf Analysevariablen übertragen werden. Der Custom Link-Ansatz sollte als eine Verschlankung und Vereinfachung sowohl der Implementierung als auch der erfassten Daten betrachtet werden. Bei der Custom Link-Lösung sind keine Variablen oder Methoden für die Videomessung vordefiniert, sondern es ist eine vollständige anwenderdefinierte Einrichtung erforderlich. Es sollte möglich sein, den Player-Ereigniscode zu aktualisieren, um auf die anwenderdefinierten Linktracking-Aufrufe für grundlegende Spielereignisse wie Start und Ende zu verweisen. Siehe [Custom Link-Implementierungsleitfaden](/help/measurement-options/cl-in-aa/cl-impl-guide.md) und [Manuelles Linktracking mithilfe des benutzerdefinierten Link-Codes](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) für weitere Details.

Die folgenden Tabellen enthalten Übersetzungen zwischen der Milestone-Lösung und der Custom Link-Lösung.

## Migrationsleitfaden {#section_btt_fc2_dfb}

### Videovariablenreferenz

<table>
<thead>
<tr>
<th><strong>Milestone-Metrik</strong></th>
<th><strong>Variablentyp</strong></th>
<th><strong>Anwenderspezifischer Link</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Inhalt</td>
<td>
<p>eVar</p>
<p>Standardgültigkeit: Besuch</p>
</td>
<td>Festlegung eines eigenen eVars</td>
</tr>
<tr>
<td>Content-Typ</td>
<td>
<p>eVar</p>
<p>Standardgültigkeit: Seitenansicht</p>
</td>
<td>Festlegung eines eigenen eVars</td>
</tr>
<tr>
<td>Inhaltsbesuchszeit</td>
<td>
<p>Ereignis-</p>
<p>Typ: Zähler</p>
</td>
<td>Festlegung eines eigenen Ereignisses</td>
</tr>
<tr>
<td>Videoaufrufe</td>
<td>
<p>Ereignis-</p>
<p>Typ: Zähler</p>
</td>
<td>Festlegung eines eigenen Ereignisses</td>
</tr>
<tr>
<td>Videobeendigungen</td>
<td>
<p>Ereignis-</p>
<p>Typ: Zähler</p>
</td>
<td>Festlegung eines eigenen Ereignisses</td>
</tr>
</tbody>
</table>

### Medienmodulvariablen

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone-Syntax
</th>
<th>Benutzerspezifischer Link
</th>
<th>Benutzerspezifischer Link  Syntax
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData["video.name"] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = { "a.media.name":
    "eVar2,prop2", "a.media.segment":
    "eVar3", "a.contentType":
    "eVar1", "a.media.timePlayed":
    "event3", "a.media.view":
    "event1", "a.media.segmentView":
    "event2", "a.media.complete":
    "event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>nicht angegeben
</td>
<td>Die Zuordnung von Kontextdaten zu eVars, Props und Ereignissen erfolgt nun durch Verarbeitungsregeln.
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
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
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
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone-Syntax
</th>
<th>Benutzerspezifischer Link
</th>
<th>Benutzerspezifischer Link  Syntax
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData["video.name"] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segment View":"event2", "a.media.complete":"event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>nicht angegeben
</td>
<td>Die Zuordnung von Kontextdaten zu eVars, Props und Ereignissen erfolgt nun durch Verarbeitungsregeln.
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
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
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
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
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
<th>Benutzerspezifischer Link
</th>
<th>Benutzerspezifischer Link  Syntax
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
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
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
<td>nicht verfügbar
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
Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer-Name";
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
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
<td>nicht verfügbar
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
<td>nicht verfügbar
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
<th>Benutzerspezifischer Link
</th>
<th>Benutzerspezifischer Link  Syntax
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
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
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
<td>nicht verfügbar
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
<td>nicht verfügbar
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
<td>nicht verfügbar
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
<th>Benutzerspezifischer Link
</th>
<th>Benutzerspezifischer Link  Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.video.name, contextData.video.view';
s.linkTrackEvents = 'event2';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event2';
s.contextData['video.name'] = mediaName;
s.contextData['video.view'] = 'true';
s.tl(this,'o','Videostart');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b></b> mediaName: (Erforderlich) Der Name des Videos, wie er in Videoberichten angezeigt werden soll.</td>
<td>Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b></b> mediaLength: (Erforderlich) Die Länge des Videos in Sekunden.
</td>
<td>
Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf
</td>
<td>
<pre>
s.contextData['video.length'] ="90";
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b></b> mediaPlayerName: (Erforderlich) Der Name des Medienplayers, der zum Anzeigen des Videos verwendet wird, wie er in Videoberichten angezeigt werden soll.
</td>
<td>
Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer-Name";
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
<td>nicht angegeben
</td>
<td>nicht verfügbar</td>
</tr>
<tr>
<td>name</td>
<td><b></b> name: (erforderlich) Name oder ID der Anzeige.</td>
<td>nicht angegeben</td>
<td>nicht verfügbar</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b></b> length: (Erforderlich) Die Länge der Anzeige.
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b></b> playerName: (Erforderlich) Der Name des Medienplayers, der zum Anzeigen der Anzeige verwendet wird.
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName</b>: Name oder ID des Hauptinhalts, in den die Anzeige eingebettet ist.
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod</b>: Die Position im Hauptinhalt, an der die Anzeige wiedergegeben wurde.
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition</b>: Die Position in der Werbeunterbrechung, an der die Anzeige wiedergegeben wurde.
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM</b>: CPM oder verschlüsselter CPM (mit „~“ als Präfix) für diese Wiedergabe.
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
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
<td>
<pre>
s.tl()
</pre>
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
<td>nicht angegeben
</td>
<td>nicht verfügbar
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
s.tl()
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.complete';
s.linkTrackEvents = 'event3';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event3';
s.contextData['video.name'] = mediaName;
s.contextData['video.complete'] = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>nicht angegeben 
</td>
<td>nicht verfügbar
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>nicht angegeben
</td>
<td>nicht verfügbar
</td>
</tr>
</tbody>
</table>

