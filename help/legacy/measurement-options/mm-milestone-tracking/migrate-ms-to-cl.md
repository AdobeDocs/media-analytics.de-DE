---
title: Erfahren Sie mehr über die Migration vom Meilenstein zum benutzerspezifischen Link
description: Erfahren Sie, wie Sie Meilenstein-Variablen in Methoden des Moduls „Benutzerspezifischer Link“ und „Meilenstein“ in die Syntax für benutzerspezifische Links ändern.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/VrVa44XnAVGI2kNPEFfTB2S840O8jQdvI-PuGX5Y3nM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 598
ht-degree: 79%

---

# Migration von Milestone zu Custom Link{#migrating-from-milestone-to-custom-link}

## Überblick {#overview}

Die Kernkonzepte der Videomessung sind für das Meilenstein- und das Tracking benutzerdefinierter Links identisch, bei denen Video-Player-Ereignisse mit Analysemethoden verknüpft und gleichzeitig Player-Metadaten und -Werte erfasst und Analytics-Variablen zugeordnet werden. Der Ansatz für benutzerspezifische Links sollte als eine Verschlankung und Vereinfachung sowohl der Implementierung als auch der erfassten Daten betrachtet werden. Bei der Lösung „Benutzerspezifischer Link“ sind keine Variablen oder Methoden für die Videomessung vordefiniert, sondern eine vollständige benutzerdefinierte Einrichtung erforderlich. Es sollte möglich sein, den Player-Ereigniscode so zu aktualisieren, dass er auf die benutzerdefinierten Linktracking-Aufrufe für grundlegende Player-Ereignisse wie Start und Abschluss verweist. Weitere Informationen finden Sie im [Implementierungshandbuch für benutzerspezifische Links](/help/legacy/measurement-options/cl-in-aa/cl-impl-guide.md).

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

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Syntax benutzerdefinierter Links |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | nicht angegeben | Die Zuordnung von Kontextdaten zu eVars, Props und Ereignissen erfolgt nun durch Verarbeitungsregeln. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Optionale Variablen

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Syntax benutzerdefinierter Links |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | nicht angegeben | Nicht verfügbar. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | nicht angegeben | Nicht verfügbar. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | nicht angegeben | Nicht verfügbar. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | nicht angegeben | Nicht verfügbar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | nicht angegeben | Nicht verfügbar. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | nicht angegeben | Nicht verfügbar. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |

### Anzeigenverfolgungsvariablen

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Syntax benutzerdefinierter Links |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | nicht angegeben | Nicht verfügbar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | nicht angegeben | Nicht verfügbar. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | nicht angegeben | Nicht verfügbar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | nicht angegeben | Nicht verfügbar. |

### Medienmodulmethoden

| Milestone | Milestone-Syntax | Benutzerspezifischer Link | Syntax benutzerdefinierter Links |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName` (erforderlich): Der Name des Videos, wie er in Videoberichten angezeigt werden soll. | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength` (erforderlich): Die Länge des Videos in Sekunden. | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.contextData['video.length']` <br> `  = "90";` |
| mediaPlayerName | `mediaPlayerName` (erforderlich): Der Name des Medien-Players, mit dem das Video wiedergegeben wird, wie er in Videoberichten angezeigt werden soll. | Setzen von eVar- oder Kontextdatenvariablen im Link-Aufruf. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | nicht angegeben | Nicht verfügbar. |
| name | `name` (erforderlich): Name oder ID der Anzeige. | nicht angegeben | Nicht verfügbar. |
| length | `length` (erforderlich): Länge der Anzeige. | nicht angegeben | Nicht verfügbar. |
| playerName | `playerName` (erforderlich): Name des Medien-Players, mit dem die Anzeige wiedergegeben wird. | nicht angegeben | Nicht verfügbar. |
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
