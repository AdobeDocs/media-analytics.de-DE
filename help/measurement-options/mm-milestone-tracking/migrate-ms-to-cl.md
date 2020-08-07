---
title: Migration von Milestone zu Custom Link
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: ht
source-git-commit: e25c4d0add969ad31393f2eeb33b1a12b7205586
workflow-type: ht
source-wordcount: '576'
ht-degree: 100%

---


# Migration von Milestone zu Custom Link {#migrating-from-milestone-to-custom-link}

## Überblick {#overview}

Die grundlegenden Prinzipien der Videomessung sind die gleichen wie beim Milestone- und Custom Link-Tracking, bei denen Videoplayer-Ereignisse aufgenommen und auf Analysemethoden übertragen werden, während gleichzeitig Playermetadaten und -werte erfasst und auf Analysevariablen übertragen werden. Der Custom Link-Ansatz sollte als eine Verschlankung und Vereinfachung sowohl der Implementierung als auch der erfassten Daten betrachtet werden. Bei der Custom Link-Lösung sind keine Variablen oder Methoden für die Videomessung vordefiniert, sondern es ist eine vollständige anwenderdefinierte Einrichtung erforderlich. Es sollte möglich sein, den Player-Ereigniscode zu aktualisieren, um auf die anwenderdefinierten Linktracking-Aufrufe für grundlegende Spielereignisse wie Start und Ende zu verweisen. Weitere Informationen finden Sie im [Implementierungshandbuch für benutzerspezifische Links](/help/measurement-options/cl-in-aa/cl-impl-guide.md).

Die folgenden Tabellen enthalten Übersetzungen zwischen der Milestone-Lösung und der Lösung mit benutzerspezifischen Links.

## Migrationsleitfaden {#migration-guide}

### Videovariablenreferenz

| Milestone-Metrik | Variablentyp | Benutzerspezifischer Link |
| --- | --- | --- |
| Inhalt | eVar <br>Standardgültigkeit: Besuch | Festlegung einer eigenen eVar. |
| Content-Typ | eVar <br>Standardgültigkeit: Seitenansicht | Festlegung einer eigenen eVar. |
| Inhaltsbesuchszeit | Ereignistyp: <br>Zähler | Festlegung eines eigenen Ereignisses. |
| Videoaufrufe | Ereignistyp: <br>Zähler | Festlegung eines eigenen Ereignisses. |
| Videobeendigungen | Ereignistyp: <br>Zähler | Festlegung eines eigenen Ereignisses. |

### Medienmodulvariablen

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Benutzerspezifischer Link Syntax |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | nicht angegeben | Die Zuordnung von Kontextdaten zu eVars, Props und Ereignissen erfolgt nun durch Verarbeitungsregeln. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Optionale Variablen

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Benutzerspezifischer Link Syntax |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | nicht angegeben | Nicht verfügbar. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | nicht angegeben | Nicht verfügbar. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | nicht angegeben | Nicht verfügbar. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | nicht angegeben | Nicht verfügbar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | nicht angegeben | Nicht verfügbar. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | nicht angegeben | Nicht verfügbar. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |

### Anzeigenverfolgungsvariablen

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Benutzerspezifischer Link Syntax |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | nicht angegeben | Nicht verfügbar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | nicht angegeben | Nicht verfügbar. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | nicht angegeben | Nicht verfügbar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |

### Medienmodulmethoden

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Benutzerspezifischer Link Syntax |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName` (erforderlich): Der Name des Videos, wie er in Videoberichten angezeigt werden soll. | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength` (erforderlich): Die Länge des Videos in Sekunden. | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName` (erforderlich): Der Name des Medien-Players, mit dem das Video wiedergegeben wird, wie er in Videoberichten angezeigt werden soll. | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | nicht angegeben | Nicht verfügbar. |
| name | `name` (erforderlich): Name oder ID der Anzeige. | nicht angegeben | Nicht verfügbar. |
| length | `length` (erforderlich): Länge der Anzeige. | nicht angegeben | Nicht verfügbar. |
| playerName | `playerName` (erforderlich): Name des Median-Players, mit dem die Anzeige wiedergegeben wird. | nicht angegeben | Nicht verfügbar. |
| parentName | `parentName`: Name oder ID des Hauptinhalts, in den die Anzeige eingebettet ist. | nicht angegeben | Nicht verfügbar. |
| parentPod | `parentPod`: Die Position im Hauptinhalt, an der die Anzeige wiedergegeben wurde. | nicht angegeben | Nicht verfügbar. |
| parentPodPosition | `parentPodPosition`: Die Position in der Werbeunterbrechung, an der die Anzeige wiedergegeben wurde. | nicht angegeben | Nicht verfügbar. |
| CPM | `CPM`: CPM oder verschlüsselter CPM (mit „~“ als Präfix) für diese Wiedergabe. | nicht angegeben | Nicht verfügbar. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Verwenden Sie für das Tracking von Klicks einen benutzerspezifischen Link-Analyseaufruf. |
| Media.close | `s.Media.close(mediaName)` | nicht angegeben | Nicht verfügbar. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | nicht angegeben | Nicht verfügbar. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | nicht angegeben | Nicht verfügbar. |
| Media.monitor | `s.Media.monitor(s, media)` | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | nicht angegeben | Nicht verfügbar. |
