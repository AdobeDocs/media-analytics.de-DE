---
title: Zuordnung von Media Analytics-Parametern für Adobe Experience Platform und Customer Journey Analytics
description: XDM-Feldpfad-Zuordnung für Media Analytics-Parameter, die mit dem Analytics Source Connector und Customer Journey Analytics verwendet werden.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 1331
ht-degree: 20%

---

# Zuordnung von Media Analytics-Parametern für Adobe Experience Platform und Customer Journey Analytics

Dieses Dokument enthält eine umfassende Liste aller Medienanalyseparameter, die in Adobe Experience Platform und Customer Journey Analytics verwendet werden. Sie unterstützt die Integration von Daten, die von Adobe Analytics über den [Analytics Source Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/analytics) oder den [Analytics Source Connector for Classifications) in Platform importiert &#x200B;](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/classifications), indem jeder Parameter seinem entsprechenden XDM-Feldpfad zugeordnet wird.

>[!NOTE]
>
>Dieser Verweis gilt für Unternehmen, die den [Analytics-Quell-Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/analytics) verwenden, um Streaming-Mediendaten aus Adobe Analytics zur Verwendung mit Customer Journey Analytics-Berichten oder anderen Platform-Services in Adobe Experience Platform zu übertragen. Diese Änderungen wirken sich nicht auf Adobe Analytics als eigenständige Anwendung aus, einschließlich Datenerfassung, Verarbeitung und Reporting.

## In Media Analytics reservierte Variablen

Seit Oktober 2025 wird der `media.mediaTimed` XDM-Feldpfad, der vom Analytics-Quell-Connector verwendet wird, vollständig eingestellt und durch `mediaReporting` ersetzt. Daten, die nach Oktober 2025 aufgenommen werden, enthalten nur `mediaReporting` Felder. Frühere Daten bleiben unter dem Pfad des alten Felds verfügbar, der in den Tabellen unten unter dem Pfad **Legacy-XDM-Feld** dargestellt wird.

### Keep-Alive-Aufrufverhalten

Mit dem Analytics-Quell-Connector für Streaming-Medien werden jetzt Keep-Alive-Aufrufe aus Adobe Analytics in Adobe Experience Platform aufgenommen. Dies kann sich auf Customer Journey Analytics-Berichte auswirken:

* **Sitzungsanzahl**: Keep-Alive-Aufrufe unterstützen die Aufrechterhaltung aktiver Benutzersitzungen auch ohne direkte Medieninteraktionen. Diese Aufrufe werden alle 20 Minuten nach dem letzten Ereignis pro Medienwiedergabe generiert. Um eine optimale Sitzungsverfolgung zu gewährleisten, konfigurieren Sie den Besuchsablauf auf 30 Minuten in der Datenansicht.

* **Anzahl der Ereignisse**: Keep-Alive-Aufrufe werden jetzt für die Metrik Customer Journey Analytics-Ereignisse gezählt. Um sie auszuschließen, erstellen Sie einen Filter, der Ereignisse mit Ereignistyp `media.keepalive` ausschließt.

## Streaming-Medienparameter

| Feldname | Legacy-XDM-Feld | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Stream-Typ]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | Dimension | [[!UICONTROL Stream-Typ]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL Inhalts-ID]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | Dimension | [[!UICONTROL Inhalts-ID]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL Inhaltslänge]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | Dimension | [[!UICONTROL Inhaltslänge]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL Content-Typ]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | Dimension | [[!UICONTROL Content-Typ]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL Mediensitzungs-ID]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | Dimension | [[!UICONTROL Mediensitzungs-ID]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL Name des Inhalts-Players]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | Dimension | [[!UICONTROL Name des Inhalts-Players]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL Inhaltskanal]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | Dimension | [[!UICONTROL Inhaltskanal]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL Inhaltssegment]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | Dimension | [[!UICONTROL Inhaltssegment]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL Inhaltsname]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | Dimension | [[!UICONTROL Inhaltsname]](/help/reporting/dimensions/content-name.md) | |
| Videopfad | *Wird in AEP/CJA nicht verwendet* | | | | Adobe Analytics-spezifische Eigenschaft |
| [[!UICONTROL Anzeigen]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | Dimension | [[!UICONTROL Anzeigen]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL Staffel]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | Dimension | [[!UICONTROL Staffel]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL Folge]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | Dimension | [[!UICONTROL Folge]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL Genre]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | Dimension | Nicht unterstützt | `mediaReporting` verwenden |
| [[!UICONTROL Netzwerk]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | Dimension | [[!UICONTROL Netzwerk]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL Sendungstyp]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | Dimension | [[!UICONTROL Sendungstyp]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | Dimension | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL Autorisiert]](/help/reporting/metrics/authorized.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | Dimension | [[!UICONTROL Autorisiert]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL Day Part]](/help/reporting/dimensions/day-part.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | Dimension | [[!UICONTROL Day Part]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL Medien-Feed-Typ]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | Dimension | [[!UICONTROL Medien-Feed-Typ]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL Künstler]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | Dimension | [[!UICONTROL Künstler]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL Album]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | Dimension | [[!UICONTROL Album]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL Beschriftung]](/help/reporting/dimensions/label.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`sessionDetails.label` | Dimension | [[!UICONTROL Beschriftung]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL author]](/help/reporting/dimensions/author.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`sessionDetails.author` | Dimension | [[!UICONTROL author]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL Station]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | Dimension | [[!UICONTROL Station]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL Veröffentlicher]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | Dimension | [[!UICONTROL Veröffentlicher]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | Metrik | [[!UICONTROL Medienstarts]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL Inhaltsstarts]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | Metrik | [[!UICONTROL Inhaltsstarts]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL Inhalt abgeschlossen]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | Metrik | [[!UICONTROL Inhalt abgeschlossen]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL Besuchszeit für Inhalt]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | Metrik | [[!UICONTROL Besuchszeit für Inhalt]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL Besuchszeit für Medien]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | Metrik | [[!UICONTROL Besuchszeit für Medien]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL Eindeutige Wiedergabezeit]](/help/reporting/metrics/unique-time-played.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | Metrik | [[!UICONTROL Eindeutige Wiedergabezeit]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL 10%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | Metrik | [[!UICONTROL 10%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 25%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | Metrik | [[!UICONTROL 25%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 50%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | Metrik | [[!UICONTROL 50%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 75 % Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | Metrik | [[!UICONTROL 75 % Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 95%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | Metrik | [[!UICONTROL 95%-Fortschrittsmarkierung]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Zielgruppendurchschnitt pro Minute]](/help/reporting/metrics/average-minute-audience.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | Metrik | [[!UICONTROL Zielgruppendurchschnitt pro Minute]](/help/reporting/metrics/average-minute-audience.md) | |
| Sekunden seit dem letzten Aufruf | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | Metrik | Sekunden seit dem letzten Aufruf | |
| [[!UICONTROL Betroffene Streams angehalten]](/help/reporting/metrics/paused-impacted-streams.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | Metrik | [[!UICONTROL Betroffene Streams angehalten]](/help/reporting/metrics/paused-impacted-streams.md) | Wir erfassen mediaTimed durch Berechnung dieses Werts aus anderen Ereignissen |
| [[!UICONTROL Ereignisse anhalten]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | Metrik | [[!UICONTROL Ereignisse anhalten]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL Pausierung insgesamt]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | Metrik | [[!UICONTROL Pausierung insgesamt]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL Inhaltswiederaufnahmen]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | Metrik | [[!UICONTROL Inhaltswiederaufnahmen]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL Inhaltssegmentansichten]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | Metrik | [[!UICONTROL Inhaltssegmentansichten]](/help/reporting/metrics/content-segment-views.md) | |

## Aktualisierung der Player-Statusparameter

| Feldname | Legacy-XDM-Feld | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
| --- | --- | --- | --- | --- | --- |
| Von Player-Status betroffene Streams | Nicht unterstützt | `xdm.mediaReporting.`<br>`states.isSet` | Metrik | Nicht unterstützt | `mediaReporting` verwenden |
| Anzahl der Player-Status | Nicht unterstützt | `xdm.mediaReporting.`<br>`states.count` | Metrik | Nicht unterstützt | `mediaReporting` verwenden |
| Gesamtdauer der Player-Status | Nicht unterstützt | `xdm.mediaReporting.`<br>`states.time` | Metrik | Nicht unterstützt | `mediaReporting` verwenden |
| Player-Statusname | Nicht unterstützt | `xdm.mediaReporting.`<br>`states.name` | Dimension | Nicht unterstützt | `mediaReporting` verwenden |

## Kapitelparameter

| Feldname | Legacy-XDM-Feld | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Kapitel]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | Dimension | [[!UICONTROL Kapitel]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL Kapitelstart]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | Metrik | [[!UICONTROL Kapitelstart]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL Kapitel abgeschlossen]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | Metrik | [[!UICONTROL Kapitel abgeschlossen]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL Besuchszeit für Kapitel]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | Metrik | [[!UICONTROL Besuchszeit für Kapitel]](/help/reporting/metrics/chapter-time-spent.md) | |

## Anzeigenparameter

| Feldname | Legacy-XDM-Feld | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitetes Feld | Hinweise |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Werbe-ID]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | Dimension | [[!UICONTROL Werbe-ID]](/help/reporting/dimensions/ad.md) | |
| [[!UICONTROL Anzeige in Position Pod]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | Dimension | [[!UICONTROL Anzeige in Position Pod]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL Anzeigenlänge]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | Metrik | [[!UICONTROL Anzeigenlänge]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL Anzeigenplayer-Name]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | Dimension | [[!UICONTROL Anzeigenplayer-Name]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL Werbeunterbrechungs-ID]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | Dimension | [[!UICONTROL Werbeunterbrechungs-ID]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL Anzeigenname]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | Dimension | [[!UICONTROL Anzeigenname]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL Advertiser]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | Dimension | [[!UICONTROL Advertiser]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL Kampagnen-ID]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | Dimension | [[!UICONTROL Kampagnen-ID]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL Ad Start]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | Metrik | [[!UICONTROL Ad Start]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL Ad Complete]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | Metrik | [[!UICONTROL Ad Complete]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL Besuchszeit für Anzeige]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | Metrik | [[!UICONTROL Besuchszeit für Anzeige]](/help/reporting/metrics/ad-time-spent.md) | |

## Qualitätsparameter

| Feldname | Legacy-XDM-Feld | XDM-Feldpfad für Berichterstellung | Datentyp | Abgeleitete Felder | Hinweise |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Durchschnittliche Bitrate]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | Beide | [[!UICONTROL Durchschnittliche Bitrate]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL Zeit bis zum Start]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | Beide | [[!UICONTROL Zeit bis zum Start]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL Dropped Frames]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | Beide | [[!UICONTROL Dropped Frames]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL Pufferereignisse]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | Beide | [[!UICONTROL Pufferereignisse]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL Gesamtdauer des Puffers]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | Beide | [[!UICONTROL Gesamtdauer des Puffers]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL Bitratenänderungen]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | Beide | [[!UICONTROL Bitratenänderungen]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL Fehler/Fehlerereignisse]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | Beide | [[!UICONTROL Fehler/Fehlerereignisse]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL Player SDK-Fehler-IDs]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | Dimension | Nicht unterstützt | `mediaReporting` verwenden |
| [[!UICONTROL Externe Fehler-IDs]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | Dimension | Nicht unterstützt | `mediaReporting` verwenden |
| [[!UICONTROL Drops vor Start]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | Metrik | [[!UICONTROL Drops vor Start]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL Vom Puffer betroffene Streams]](/help/reporting/metrics/buffer-impacted-streams.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | Metrik | [[!UICONTROL Vom Puffer betroffene Streams]](/help/reporting/metrics/buffer-impacted-streams.md) | Aus anderen Ereignissen berechnet |
| [[!UICONTROL Von Bitratenänderung betroffene Streams]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | Metrik | [[!UICONTROL Von Bitratenänderung betroffene Streams]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | Aus anderen Ereignissen berechnet |
| [[!UICONTROL Von Fehlern betroffene Streams]](/help/reporting/metrics/error-impacted-streams.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | Metrik | [[!UICONTROL Von Fehlern betroffene Streams]](/help/reporting/metrics/error-impacted-streams.md) | Aus anderen Ereignissen berechnet |
| [[!UICONTROL Von Dropped Frames betroffene Streams]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | Nicht unterstützt | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | Metrik | [[!UICONTROL Von Dropped Frames betroffene Streams]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | Aus anderen Ereignissen berechnet |

## Media Analytics-Klassifizierungen

Media Analytics-Klassifizierungen werden über einen separaten Fluss namens ACDC in AEP aufgenommen. Jede in der folgenden Tabelle aufgeführte Klassifizierungsgruppe entspricht einem eindeutigen Datensatz in AEP. In CJA ist es erforderlich, eine Verbindung zwischen dem Media Analytics-Ereignisdatensatz und den einzelnen Klassifizierungsdatensätzen herzustellen.

### Verbinden von Datensätzen in Customer Journey Analytics

So richten Sie die Verbindung in Customer Journey Analytics ein:

* Navigieren Sie zur Registerkarte **Verbindungen** und wählen Sie **Neue Verbindung erstellen** aus.
* Wählen Sie in der Verbindungsschnittstelle **Datensätze hinzufügen** und suchen Sie den Media Analytics-Ereignisdatensatz (der zum Importieren von Mediendaten über ADC verwendet wird) zusammen mit den vier relevanten Klassifizierungsdatensätzen.

### Konfigurationsdetails

Konfigurieren Sie für jeden Lookup-Datensatz (Klassifizierungsdatensatz) Folgendes:

* **Videodatensatz**:
   * Schlüssel: `_sandbox.key`
   * Passender Schlüssel: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * Datenquellentyp: `Web Data`

* **Videoad-Datensatz**:
   * Schlüssel: `_sandbox.key`
   * Passender Schlüssel: `Ad ID (advertising.adAssetReference._id)`
   * Datenquellentyp: `Web Data`

* **videoadpod-Datensatz**:
   * Schlüssel: `_sandbox.key`
   * Passender Schlüssel: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * Datenquellentyp: `Web Data`

* **VideoChapter-Datensatz**:
   * Schlüssel: `_sandbox.key`
   * Passender Schlüssel: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * Datenquellentyp: `Web Data`

### Überlegungen zum Reporting

Beim Arbeiten mit den Klassifizierungsdatensätzen während des Reportings müssen Sie sicherstellen, dass Sie auf die klassifizierungsspezifischen Feldpfade (`ACDC XDM Path`) anstatt auf die standardmäßigen Media Analytics-XDM-Felder verweisen.

## Klassifizierungstabelle

| Klassifizierungsname (Gruppe) | Feldname | ACDC XDM-Pfad |
| --- | --- | --- |
| video | Schlüssel/Asset-ID | `xdm.<_sandbox>.key` |
| video | Videolänge | `xdm.<_sandbox>.video_length` |
| video | Videoname | `xdm.<_sandbox>.video_name` |
| video | [[!UICONTROL Asset-ID]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| video | [[!UICONTROL Datum der Erstausstrahlung]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| video | [[!UICONTROL Erstes digitales Datum]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| video | [[!UICONTROL Inhaltsbewertung]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| video | [[!UICONTROL Urheber]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | Schlüssel/Werbe-ID | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL Anzeigenlänge]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL Anzeigenname]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative-ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | Schlüssel/Werbe-Pod-ID | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL Pod-Position]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL Pod-Name]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | Schlüssel/Kapitel | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL Kapitellänge]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL Kapitelversatz]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL Kapitelposition]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL Kapitelname]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Benutzerdefinierte Media Analytics-Variablen

In Adobe Analytics werden benutzerdefinierte Variablen abhängig von den in den einzelnen Report Suites definierten Implementierungsregeln verschiedenen Ereignissen oder eVars zugewiesen. Wenn diese benutzerdefinierten Variablen in Adobe Experience Platform (AEP) importiert werden, werden sie daher verschiedenen XDM-Pfaden zugeordnet.

* Ereignisse werden unter dem Pfad gespeichert:

  `_experience.analytics.event<x>to<y>.event<number>.value`

* eVars werden unter dem Pfad gespeichert:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

In beiden Fällen entspricht die `<number>` der spezifischen Ereignis- oder eVar-Nummer, die in der ursprünglichen Report Suite-Konfiguration von Adobe Analytics verwendet wurde.

### Benutzerdefinierte Variablen

| Feldname | XDM-Pfad | Datentyp |
| --- | --- | --- |
| [[!UICONTROL Medien heruntergeladen-Flag]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
| SDK-Version | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| Media Library-Version | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Stream-Format]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Datum der Erstausstrahlung]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Erstes digitales Datum]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Verknüpfte Daten]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>und<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Beide |
| [[!UICONTROL Geschätzte Streams]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
| [[!UICONTROL Anzahl der Anzeigen]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
| [[!UICONTROL Kapitelanzahl]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
| [[!UICONTROL Creative-ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Site-ID]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Creative-URL]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Platzierungs-ID]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| Frames pro Sekunde | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>und<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Beide |
| Medien-SDK Fehler-IDs | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
| [[!UICONTROL Betroffene Streams verzögern]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
| [[!UICONTROL Verzögerte &#x200B;]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
| [[!UICONTROL Gesamtdauer der Verzögerung]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrik |
