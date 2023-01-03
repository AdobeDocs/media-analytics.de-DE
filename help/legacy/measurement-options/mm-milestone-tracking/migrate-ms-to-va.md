---
title: Erfahren Sie, wie Sie von Meilenstein zu Media Analytics migrieren.
description: Erfahren Sie, wie Sie Meilenstein-Variablen in Media Analytics-Metriken und Meilenstein-Modulmethoden in Media Analytics-Syntax ändern.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 9ba64b68efec5dd8b52010ac1a13afd7703448d0
workflow-type: ht
source-wordcount: '690'
ht-degree: 100%

---

# Migration von Milestone zu Media Analytics {#migrating-from-milestone-to-media-analytics}

## Überblick  {#overview}

Die Hauptkonzepte der Videomessung sind bei Milestone und Media Analytics identisch. Dabei werden Videoplayer-Ereignisse verwendet und Analysemethoden zugeordnet. Außerdem werden Player-Metadaten und -Werte erfasst und Analytics-Variablen zugeordnet. Die Media Analytics-Lösung wurde aus Milestone entwickelt. Viele der Methoden und Metriken sind identisch. Konfigurationsansätze und Code wurden jedoch erheblich geändert. Es sollte möglich sein, den Player-Ereignis-Code so zu aktualisieren, dass er auf die neuen Media Analytics-Methoden verweist. Weitere Informationen zur Implementierung von Media Analytics finden Sie unter [SDK-Übersicht](/help/legacy/setup/legacy-setup-overview.md) und [Tracking-Übersicht](/help/use-cases/track-av-playback/track-core-overview.md).

Die folgenden Tabellen enthalten Übersetzungen zwischen der Milestone- und der Media Analytics-Lösung.

## Migrationsleitfaden {#migration-guide}

### Variablenreferenz

| Milestone-Metrik | Variablentyp | Media Analytics-Metrik |
| --- | --- | --- |
| Inhalt | eVar <br>Standardgültigkeit: Besuch | Inhalt |
| Content-Typ | eVar <br>Standardgültigkeit: Seitenansicht | Content-Typ |
| Inhaltsbesuchszeit | Ereignistyp: <br>Zähler | Inhaltsbesuchszeit |
| Videoaufrufe | Ereignistyp: <br>Zähler | Videoaufrufe |
| Videobeendigungen | Ereignistyp: <br>Zähler | Inhaltsbeendigung |


### Medienmodulvariablen

| Milestone | Milestone-Syntax | Media Analytics | Syntax von Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | nicht angegeben | Alle Medienanalysedaten werden nur mit Kontextdaten gesendet. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | nicht angegeben | Media Analytics-Kontextdaten werden automatisch in reservierte Variablen eingetragen. Zuordnung zu eVars, Requisiten und Ereignissen ist innerhalb des Implementierungscodes nicht mehr erforderlich. Kontextdaten können Verarbeitungsregeln anhand von Variablen zugeordnet werden. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | nicht angegeben | Nicht mehr benötigt, da die Zuordnung über reservierte Variablen und Verarbeitungsregeln erfolgt. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | nicht angegeben | Nicht mehr benötigt, da die Zuordnung über reservierte Variablen und Verarbeitungsregeln erfolgt. |

### Optionale Variablen

| Milestone | Milestone-Syntax | Media Analytics | Syntax von Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | nicht angegeben | Wir bieten keine vordefinierten Player-Zuordnungen mehr an. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | nicht angegeben | Wir bieten keine vordefinierten Player-Zuordnungen mehr an. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | nicht angegeben | Inhaltsbeendigung unterstützt nur eine 100%ige Fortschrittsmarkierung. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | nicht angegeben | Inhaltsbeendigung unterstützt nur eine 100%ige Fortschrittsmarkierung. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK-Schlüssel: playerName;<br> API-Schlüssel: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | nicht angegeben | Media Analytics ist auf 10 Sekunden für Inhalte und 1 Sekunde für Anzeigen eingestellt. Es sind keine weiteren Optionen verfügbar. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | nicht angegeben | Media Analytics nimmt das Tracking der Fortschrittsmarkierungen immer bei 10, 25, 50, 75 und 95 % vor. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | nicht angegeben | Media Analytics nimmt das Tracking der Fortschrittsmarkierungen immer bei 10, 25, 50, 75 und 95 % vor. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | nicht angegeben | Das automatische Tracking ist nicht mehr verfügbar. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | nicht angegeben | Das automatische Tracking ist nicht mehr verfügbar. |

### Anzeigenverfolgungsvariablen

| Milestone | Milestone-Syntax | Media Analytics | Syntax von Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | nicht angegeben | Media Analytics ist auf 10 Sekunden für Inhalte und 1 Sekunde für Anzeigen eingestellt. Es sind keine weiteren Optionen verfügbar. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | nicht angegeben | Fortschrittsmarkierungen werden nicht standardmäßig für Anzeigen bereitgestellt. Verwenden Sie berechnete Metriken, um Anzeigenfortschrittsmarken zu erstellen. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | nicht angegeben | Media Analytics ist für Anzeigen auf 1 Sekunde eingestellt. Es sind keine weiteren Optionen verfügbar. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | nicht angegeben | Das automatische Tracking ist nicht mehr verfügbar. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | nicht angegeben | Das automatische Tracking ist nicht mehr verfügbar. |

### Medienmodulmethoden

| Milestone | Milestone-Syntax | Media Analytics | Syntax von Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName` (erforderlich): Der Name des Videos, wie er in Videoberichten angezeigt werden soll. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength` (erforderlich): Die Länge des Videos in Sekunden. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName` (erforderlich): Der Name des Medien-Players, mit dem das Video wiedergegeben wird, wie er in Videoberichten angezeigt werden soll. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name` (erforderlich): Name oder ID der Anzeige. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length` (erforderlich): Länge der Anzeige. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName` (erforderlich): Name des Medien-Players, mit dem die Anzeige wiedergegeben wird. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: Name oder ID des Hauptinhalts, in den die Anzeige eingebettet ist. | nicht angegeben | Automatisch geerbt. |
| parentPod | `parentPod`: Die Position im Hauptinhalt, an der die Anzeige wiedergegeben wurde. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: Die Position in der Werbeunterbrechung, an der die Anzeige wiedergegeben wurde. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: CPM oder verschlüsselter CPM (mit „~“ als Präfix) für diese Wiedergabe. | nicht angegeben | In Media Analytics nicht standardmäßig verfügbar. |
| Media.click | `s.Media.click(name, offset)` | nicht angegeben | Verwenden Sie für das Tracking von Klicks einen benutzerspezifischen Link-Analyseaufruf. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> oder <br>trackEvent | `trackPause()` <br> oder `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> oder <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Verwenden Sie zum Festlegen zusätzlicher Variablen benutzerdefinierte oder standardmäßige Metadaten. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | nicht angegeben | Die Tracking-Aufrufhäufigkeit wird automatisch festgelegt. |
