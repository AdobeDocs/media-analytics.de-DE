---
seo-title: Migration von Milestone zu Custom Link
title: Migration von Milestone zu Custom Link
uuid: 1 c 8 edde 5-0 ef 1-4 bc 0-a 62 d -1747 f 4907 f 09
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
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
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
  Contextdatamapping = {"a. media. name":
 " Evar 2, prop 2 ","
 a. media. segment ":
 " Evar 3 ","
 a. contenttype ":
 " Evar 1 ","
 a. media. timeplayed ":
 " event 3 ","
 a. media. view ":
 " event 1 ","
 a. media. segmentview ":
 " event 2 ","
 a. media. complete ":
 " event 7 ","
 a. media. milestones ": {25: " event 4 ", 50: " event 5 ", 75: " event 6 "}};
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
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
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
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s. Media. contextdatamapping = {"a. media. name": " Evar 2, prop 2 ","
 a. media. segment ": " Evar 3 ","
 a. contenttype ": " Evar 1 ","
 a. media. timeplayed ": " event 3 ","
 a. media. view ": " event 1 ","
 a. media. segmentview ": " event 2 ","
 a. media. complete ": " event 7 ","
 a. media. milestones ": {25: " event 4 ", 50: " event 5 ", 75: " event 6 "}};
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
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
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
  Completecloseoffsetthreshold
 = 1
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
s. contextdata [' video. player ']
 =» customplayer Name»;
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
  Segmentbyoffsetmilestones
 = true;
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
  Adtrackoffsetmilestones 
 = "20,40,60";
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
  Adsegmentbymilestones
 = true;
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
  Adsegmentbyoffsetmilestones
 = true;
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata. video. name,
 contextdata. video. view ';
s. linktrackevents 
 =' event 2 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 2 ';
s. contextdata [' video. name '] 
 = Medianame;
s. contextdata [' video. view '] 
 =' true ';
s. tl (this,' o ',' Video Start ');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>Medianame:</b> (Erforderlich) Der Name des Videos, der in Videoberichten angezeigt werden soll.</td>
<td>Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf</td>
<td>
<pre>
s. prop 10 = medianame;
s. evar 10 = medianame;
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>Medialength:</b> (Erforderlich) Die Länge des Videos in
Sekunden.
</td>
<td>
Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf
</td>
<td>
<pre>
s. contextdata [' video. length ']
 =» 90»;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>Mediaplayername:</b> (Erforderlich) Der Name des Medienplayers,
der zum Anzeigen des Videos verwendet wird, wie er in Videoberichten
angezeigt werden soll.
</td>
<td>
Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf
</td>
<td>
<pre>
s. contextdata [' video. player ']
 =» customplayer Name»;
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
<td><b>name:</b> (Erforderlich) Der Name oder die ID der Anzeige.</td>
<td>nicht angegeben</td>
<td>nicht verfügbar</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length:</b> (Erforderlich) Die Länge der Anzeige.
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
<b>Playername:</b> (Erforderlich) Der Name des Medienplayers, mit
dem die Anzeige angezeigt wird.
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. complete ';
s. linktrackevents 
 =' event 3 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 3 ';
s. contextdata [' video. name ']
 = medianame;
s. contextdata [' video. complete ']
 =' true ';
s. tl (this,' o ',' Video Complete ');
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
s. linktrackevents =' event 2 ';
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

