---
title: Migrieren von Audiences zum neuen Datentyp Adobe Analytics für Streaming-Medien
description: Erfahren Sie, wie Sie Audiences zum neuen Datentyp Adobe Analytics für Streaming-Medien migrieren.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
source-git-commit: 61e5279e6d53b18955424e76d05d440b83dae07e
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 47%

---

# Zuordnung von Media Analytics-Parametern für Adobe Experience Platform und Customer Journey Analytics

Dieses Dokument enthält eine umfassende Liste aller Medienanalyseparameter, die in Adobe Experience Platform und Customer Journey Analytics verwendet werden. Sie unterstützt die Integration von Daten, die von Adobe Analytics über den [Analytics Source Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/analytics) oder den [Analytics Source Connector for Classifications) in Platform importiert &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/classifications), indem jeder Parameter seinem entsprechenden XDM-Feldpfad zugeordnet wird.

## In Media Analytics reservierte Variablen

Für alle von Media Analytics reservierten Variablen finden Sie Daten, die bis (einschließlich) Mai 2025 von Adobe Analytics in AEP aufgenommen wurden, unter dem „aktuellen XDM-Feldpfad“, auf den in den folgenden Tabellen verwiesen wird.

Da die Media Analytics- und ADC-Teams derzeit an der vollständigen Migration zum „XDM-Feldpfad für Berichterstellung“ arbeiten, wird eine offizielle Kommunikation freigegeben, sobald diese Migration abgeschlossen ist und der „XDM-Feldpfad für Berichterstellung“ zur Verwendung verfügbar ist.

## Streaming-Medienparameter

| Feldname | Aktueller XDM-Feldpfad (veraltet) | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| Stream-Typ | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | Dimension | Stream-Typ |                                                                       |
| Inhalts-ID | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | Dimension | Inhalts-ID |                                                                       |
| Länge des Inhalts | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | Dimension | Länge des Inhalts |                                                                       |
| Content-Typ | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | Dimension | Content-Typ |                                                                       |
| Mediensitzungs-ID | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | Dimension | Mediensitzungs-ID |                                                                       |
| Inhalts-Player-Name | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | Dimension | Inhalts-Player-Name |                                                                       |
| Inhaltskanal | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | Dimension | Inhaltskanal |                                                                       |
| Inhaltssegment | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | Dimension | Inhaltssegment |                                                                       |
| Inhaltsname | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | Dimension | Inhaltsname |                                                                       |
| Videopfad | *Wird in AEP/CJA nicht verwendet* |                                                   |           |                   | Adobe Analytics-spezifische Eigenschaft |
| Serie | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | Dimension | Serie |                                                                       |
| Staffel | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | Dimension | Staffel |                                                                       |
| Folge | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | Dimension | Folge |                                                                       |
| Genre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | Dimension | Nicht unterstützt | MediaReporting-Feld verwenden |
| Netzwerk | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | Dimension | Netzwerk |                                                                       |
| Sendungstyp | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | Dimension | Sendungstyp |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | Dimension | MVPD |                                                                       |
| Autorisiert | Nicht unterstützt | mediaReporting.sessionDetails.authorized | Dimension | Autorisiert |                                                                       |
| Tagesteil | Nicht unterstützt | mediaReporting.sessionDetails.dayPart | Dimension | Tagesteil |                                                                       |
| Medien-Feed-Typ | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | Dimension | Medien-Feed-Typ |                                                                       |
| Künstler | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | Dimension | Künstler |                                                                       |
| Album | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | Dimension | Album |                                                                       |
| Beschriftung | Nicht unterstützt | mediaReporting.sessionDetails.label | Dimension | Beschriftung |                                                                       |
| Autor | Nicht unterstützt | mediaReporting.sessionDetails.author | Dimension | Autor |                                                                       |
| Station | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | Dimension | Station |                                                                       |
| Publisher | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | Dimension | Publisher |                                                                       |
| Medienstarts | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | Metrik | Medienstarts |                                                                       |
| Inhaltsstarts | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | Metrik | Inhaltsstarts |                                                                       |
| Inhaltsbeendigung | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | Metrik | Inhaltsbeendigung |                                                                       |
| Inhaltsbesuchszeit | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | Metrik | Inhaltsbesuchszeit |                                                                       |
| Besuchszeit für Medien | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | Metrik | Besuchszeit für Medien |                                                                       |
| Eindeutige Spielzeit | Nicht unterstützt | mediaReporting.sessionDetails.uniqueTimePlayed | Metrik | Eindeutige Spielzeit |                                                                       |
| 10% Fortschrittsmarkierung | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | Metrik | 10% Fortschrittsmarkierung |                                                                       |
| 25% Fortschrittsmarkierung | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | Metrik | 25% Fortschrittsmarkierung |                                                                       |
| 50 % Fortschrittsmarkierung | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | Metrik | 50 % Fortschrittsmarkierung |                                                                       |
| 75% Fortschrittsmarkierung | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | Metrik | 75% Fortschrittsmarkierung |                                                                       |
| 95% Fortschrittsmarkierung | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | Metrik | 95% Fortschrittsmarkierung |                                                                       |
| Zielgruppendurchschnitt pro Minute | Nicht unterstützt | mediaReporting.sessionDetails.averageMinuteAudience | Metrik | Zielgruppendurchschnitt pro Minute |                                                                  |
| Sekunden seit dem letzten Aufruf | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | Metrik | Sekunden seit dem letzten Aufruf |                                                              |
| Betroffene Streams pausiert | Nicht unterstützt | mediaReporting.sessionDetails.hasPauseImpactedStreams | Metrik | Betroffene Streams pausiert | Wir erfassen mediaTimed durch Berechnung dieses Werts aus anderen Ereignissen |
| Pausierung – Ereignisse | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | Metrik | Pausierung – Ereignisse |                                                                       |
| Pausierung – Gesamtdauer | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | Metrik | Pausierung – Gesamtdauer |                                                                       |
| Inhaltswiederaufnahmen | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | Metrik | Inhaltswiederaufnahmen |                                                                       |
| Ansichten des Inhaltssegments | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | Metrik | Ansichten des Inhaltssegments |                                                                     |

{style="table-layout:auto"}

## Aktualisierung der Player-Statusparameter

| Feldname | Aktueller XDM-Feldpfad (veraltet) | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| Von Player-Status betroffene Streams | Nicht unterstützt | mediaReporting.states.isSet | Metrik | Nicht unterstützt | MediaReporting-Feld verwenden |
| Anzahl der Player-Status | Nicht unterstützt | mediaReporting.states.count | Metrik | Nicht unterstützt | MediaReporting-Feld verwenden |
| Gesamtdauer der Player-Status | Nicht unterstützt | mediaReporting.states.time | Metrik | Nicht unterstützt | MediaReporting-Feld verwenden |
| Player-Statusname | Nicht unterstützt | mediaReporting.states.name | Dimension | Nicht unterstützt | MediaReporting-Feld verwenden |

{style="table-layout:auto"}

## Kapitelparameter 

| Feldname | Aktueller XDM-Feldpfad (veraltet) | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| Kapitel | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | Dimension | Kapitel |           |
| Chapter Start | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | Metrik | Chapter Start |           |
| Kapitelbeendigung | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | Metrik | Kapitelbeendigung |          |
| Besuchszeit für Kapitel | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | Metrik | Besuchszeit für Kapitel |        |

{style="table-layout:auto"}

## Anzeigenparameter 

| Feldname | Aktueller XDM-Feldpfad (veraltet) | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Anzeigen-ID | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | Dimension | Anzeigen-ID |           |
| Anzeigenposition innerhalb der Werbeunterbrechung | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | Dimension | Anzeigenposition innerhalb der Werbeunterbrechung |     |
| Anzeigenlänge | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | Metrik | Anzeigenlänge |           |
| Name des Anzeigen-Players | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | Dimension | Name des Anzeigen-Players |           |
| ID der Werbeunterbrechung | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | Dimension | ID der Werbeunterbrechung |           |
| Anzeigenname | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | Dimension | Anzeigenname |           |
| Advertiser | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | Dimension | Advertiser |           |
| Kampagnen-ID | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | Dimension | Kampagnen-ID |           |
| Werbung gestartet | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | Metrik | Werbung gestartet |           |
| Werbung beendet | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | Metrik | Werbung beendet |           |
| Besuchszeit für Anzeige | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | Metrik | Besuchszeit für Anzeige |           |

{style="table-layout:auto"}

## Qualitätsparameter 

| Feldname | Aktueller XDM-Feldpfad (veraltet) | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitete Felder | Hinweise |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Durchschnittliche Bitrate | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Beide | Durchschnittliche Bitrate |           |
| Zeit bis Start | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Beide | Zeit bis Start |           |
| Gelöschte Frames | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Beide | Gelöschte Frames |           |
| Pufferereignisse | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Beide | Pufferereignisse |           |
| Gesamtpufferdauer | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Beide | Gesamtpufferdauer |     |
| Bitratenänderungen | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Beide | Bitratenänderungen |         |
| Fehler/Fehlerereignisse | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Beide | Fehler/Fehlerereignisse |  |
| Player-SDK-Fehler-IDs | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | Dimension | Nicht unterstützt | MediaReporting-Feld verwenden |
| Externe Fehler-IDs | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | Dimension | Nicht unterstützt | MediaReporting-Feld verwenden |
| Drops vor Start | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | Metrik | Drops vor Start |     |
| Von Puffer betroffene Streams | Nicht unterstützt | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | Metrik | Von Puffer betroffene Streams | Aus anderen Ereignissen berechnet |
| Von Bitratenänderung betroffene Streams | Nicht unterstützt | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | Metrik | Von Bitratenänderung betroffene Streams | Aus anderen Ereignissen berechnet |
| Von Fehlern betroffene Streams | Nicht unterstützt | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | Metrik | Von Fehlern betroffene Streams | Aus anderen Ereignissen berechnet |
| Von Dropped Frames betroffene Streams | Nicht unterstützt | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | Metrik | Von Dropped Frames betroffene Streams | Aus anderen Ereignissen berechnet |

{style="table-layout:auto"}

## Media Analytics-Klassifizierungen

Media Analytics-Klassifizierungen werden über einen separaten Fluss namens ACDC in AEP aufgenommen. Jede in der folgenden Tabelle aufgeführte Klassifizierungsgruppe entspricht einem eindeutigen Datensatz in AEP. In CJA ist es erforderlich, eine Verbindung zwischen dem Media Analytics-Ereignisdatensatz und den einzelnen Klassifizierungsdatensätzen herzustellen.

### Verbinden von Datensätzen in Customer Journey Analytics

So richten Sie die Verbindung in Customer Journey Analytics ein:

- Navigieren Sie zur Registerkarte **Verbindungen** und wählen Sie **Neue Verbindung erstellen** aus.
- Wählen Sie in der Verbindungsschnittstelle **Datensätze hinzufügen** und suchen Sie den Media Analytics-Ereignisdatensatz (der zum Importieren von Mediendaten über ADC verwendet wird) zusammen mit den vier relevanten Klassifizierungsdatensätzen.

### Konfigurationsdetails

Konfigurieren Sie für jeden Lookup-Datensatz (Klassifizierungsdatensatz) Folgendes:

- **Videodatensatz**:
   - Schlüssel: `_sandbox.key`
   - Passender Schlüssel: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - Datenquellentyp: `Web Data`

- **Videoad-Datensatz**:
   - Schlüssel: `_sandbox.key`
   - Passender Schlüssel: `Ad ID (advertising.adAssetReference._id)`
   - Datenquellentyp: `Web Data`

- **videoadpod-Datensatz**:
   - Schlüssel: `_sandbox.key`
   - Passender Schlüssel: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - Datenquellentyp: `Web Data`

- **VideoChapter-Datensatz**:
   - Schlüssel: `_sandbox.key`
   - Passender Schlüssel: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - Datenquellentyp: `Web Data`

### Überlegungen zum Reporting

Beim Arbeiten mit den Klassifizierungsdatensätzen während des Reportings müssen Sie sicherstellen, dass Sie auf die klassifizierungsspezifischen Feldpfade (`ACDC XDM Path`) anstatt auf die standardmäßigen Media Analytics-XDM-Felder verweisen.

## Klassifizierungstabelle

| Klassifizierungsname (Gruppe) | Feldname | ACDC XDM-Pfad |
|------------|----------|-------------|
| video | Schlüssel/Asset-ID | `<_sandbox>.key` |
| video | Videolänge | `<_sandbox>.video_length` |
| video | Videoname | `<_sandbox>.video_name` |
| video | Element-ID | `<_sandbox>.asset_id` |
| video | Erstes Sendedatum | `<_sandbox>.first_air_date` |
| video | Erstes digitales Veröffentlichungsdatum | `<_sandbox>.first_digital_date` |
| video | Inhaltsbewertung | `<_sandbox>.content_rating` |
| video | Urheber | `<_sandbox>.originator` |
| videoad | Schlüssel/Werbe-ID | `<_sandbox>.key` |
| videoad | Anzeigenlänge | `<_sandbox>.ad_length` |
| videoad | Anzeigenname | `<_sandbox>.ad_name` |
| videoad | Creative-ID | `<_sandbox>.creative_id` |
| videoadpod | Schlüssel/Werbe-Pod-ID | `<_sandbox>.key` |
| videoadpod | Position der Werbeunterbrechung | `<_sandbox>.pod_position` |
| videoadpod | Name der Werbeunterbrechung | `<_sandbox>.pod_name` |
| videochapter | Schlüssel/Kapitel | `<_sandbox>.key` |
| videochapter | Kapitellänge | `<_sandbox>.chapter_length` |
| videochapter | Kapiteloffset | `<_sandbox>.chapter_offset` |
| videochapter | Kapitelposition | `<_sandbox>.chapter_position` |
| videochapter | Kapitelname | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Benutzerdefinierte Media Analytics-Variablen

In Adobe Analytics werden benutzerdefinierte Variablen abhängig von den in den einzelnen Report Suites definierten Implementierungsregeln verschiedenen Ereignissen oder eVars zugewiesen. Wenn diese benutzerdefinierten Variablen in Adobe Experience Platform (AEP) importiert werden, werden sie daher verschiedenen XDM-Pfaden zugeordnet.

- Ereignisse werden unter dem Pfad gespeichert:

  `_experience.analytics.event<x>to<y>.event<number>.value`

- eVars werden unter dem Pfad gespeichert:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

In beiden Fällen entspricht die `<number>` der spezifischen Ereignis- oder eVar-Nummer, die in der ursprünglichen Report Suite-Konfiguration von Adobe Analytics verwendet wurde.

### Benutzerdefinierte Variablen

| Feldname | XDM-Pfad | Datentyp |
|-------------|-------------|-----------|
| Markierung „Medien heruntergeladen“ | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |
| SDK-Version | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| VHL-Version | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Stream-Format | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Erstes Sendedatum | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Erstes digitales Veröffentlichungsdatum | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Verknüpfte Daten | `_experience.analytics.customDimensions.eVars.eVar<number>` und `_experience.analytics.event<x>to<y>.event<number>.value` | Beide |
| Geschätzte Streams | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |
| Anzahl der Anzeigen | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |
| Anzahl der Kapitel | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |
| Creative-ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Site-ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Creative-URL | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Platzierungs-ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Frames pro Sekunde | `_experience.analytics.customDimensions.eVars.eVar<number>` und `_experience.analytics.event<x>to<y>.event<number>.value` | Beide |
| Medien-SDK Fehler-IDs | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |
| Von Unterbrechung betroffene Streams | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |
| Unterbrechungsereignisse | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |
| Gesamt-Unterbrechungsdauer | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrik |

{style="table-layout:auto"}
