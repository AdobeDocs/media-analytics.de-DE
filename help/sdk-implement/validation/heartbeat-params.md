---
seo-title: Beschreibungen der Heartbeat-Parameter
title: Beschreibungen der Heartbeat-Parameter
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Beschreibungen der Heartbeat-Parameter{#heartbeat-parameter-descriptions}

Liste der Heartbeat-Parameter, die Adobe erfasst und auf dem Heartbeats-Server verarbeitet:

## Alle Ereignisse

| Name | erforderlich/optional | Datenquelle | Beschreibung   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | Medien-SDK | Der Typ des zu verfolgenden Ereignisses. Ereignistypen: <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | Medien-SDK | Der Zeitstempel des letzten Ereignisses mit demselben Typ in dieser Sitzung. The value is `-1` |
| `l:event:ts` | R | Medien-SDK | Der Zeitstempel des Ereignisses. |
| `l:event:duration` | R | Medien-SDK | Der Wert wird intern (in Millisekunden) von der VHL-Bibliothek und nicht vom Player festgelegt. Er wird verwendet, um am Backend Metriken zur Besuchszeit zu berechnen. `a.media.totalTimePlayed``type=play` Beispiel: Bei einigen HB, die Diesen Parameter gesendet werden, ist für bestimmte Ereignisse "0" festgelegt, da sie" state change events" (z. B. `type=complete``type=chapter_complete``type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | Die Abspielposition befindet sich zum Zeitpunkt, zu dem das Ereignis aufgezeichnet wurde, im derzeit aktiven Asset (Hauptinhalt oder Anzeige). |
| `s:event:sid` | R | Medien-SDK | Die Sitzungs-ID (eine zufällig generierte Zeichenfolge). Alle Ereignisse in einer bestimmten Sitzung (Video und Anzeigen) sollten gleich sein. |
| `l:asset:duration / l:asset:length` (Umbenannt von `length``duration` | R | `VideoInfo` | Die Videolänge des Haupt-Assets. |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | Der Publisher des Assets. |
| `s:asset:video_id` | R | `VideoInfo` | Eine ID, mit der das Video im Publisher-Katalog eindeutig identifiziert wird. |
| `s:asset:type` | R | Medien-SDK | Der Asset-Typ (Hauptinhalt oder Anzeige). |
| `s:stream:type` | R | `VideoInfo` | Der Streamtyp. Kann einer der folgenden sein: <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>. |
| `s:user:id` | O | Konfigurationsobjekt für mobile App Measurement-VisitorID | Speziell festgelegte Besucher-ID des Anwenders. |
| `s:user:aid` | O | Experience Cloud-Organisation | Der Analytics-Besucher-ID-Wert des Anwenders. |
| `s:user:mid` | R | Experience Cloud-Organisation | Der Experience Cloud-Besucher-ID-Wert des Anwenders. |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | Alle in Audience Manager festgelegten Kundenanwender-IDs. |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | Report Suite-ID (oder -IDs) | SiteCatalyst-RSID, an die Berichte gesendet werden sollen. |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | SiteCatalyst-Tracking-Server. |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | Gibt an, ob der Traffic über HTTPS (bei 1) oder HTTP (bei 0) erfolgt. |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | Legen Sie bei Primetime-Playern „primetime“ und bei anderen Playern den tatsächlichen OVP fest. |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | Die OVP-Versionszeichenfolge. |
| `s:sp:player_name` | R | `VideoInfo` | Videoplayername (die tatsächliche Player-Software, mit der der Player identifiziert wird). |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | Der Kanal, auf dem der Benutzer den Inhalt anschaut. Bei einer mobilen App ist dies der App-Name. Bei einer Website ist es der Domänenname. |
| `s:sp:hb_version` | R | Medien-SDK | Die Versionsnummer der VideoHeartbeat-Bibliothek, die den Aufruf ausgibt. |
| `l:stream:bitrate` | R | `QoSInfo` | Der aktuelle Wert der Stream-Bitrate (in bps). |

## Fehlerereignisse

| Name | erforderlich/optional | Datenquelle | Beschreibung   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | Medien-SDK | Die Quelle des Fehlers (entweder intern im Player oder auf Anwendungsebene). |
| `s:event:id` | R | Medien-SDK | Fehler-ID, mit der der Fehler eindeutig identifiziert wird. |

## Anzeigenereignisse

| Name | erforderlich/optional | Datenquelle | Beschreibung   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | Der Name der Werbeanzeige. |
| `s:asset:ad_sid` | R | Medien-SDK | Eine eindeutige Kennung, die vom Medien-SDK generiert und an alle anzeigenbezogenen Pings angehängt wird. |
| `s:asset:pod_id` | R | Medien-SDK | Werbeunterbrechungs-ID im Video. Dieser Wert wird automatisch anhand der folgenden Formel berechnet: `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | Index der Anzeige innerhalb der Werbeunterbrechung (die erste Anzeige hat den Index 0, die zweite Anzeige den Index 1 usw.). |
| `s:asset:resolver` | R | `AdBreakInfo` | Der Anzeigen-Resolver. |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | Die anwenderspezifischen Anzeigenmetadaten. |

## Kapitelereignisse

| Name | erforderlich/optional | Datenquelle | Beschreibung   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | Medien-SDK | Die eindeutige ID, die mit der Wiedergabeinstanz des Kapitels verknüpft ist.  Hinweis: Ein Kapitel kann mehrmals wiedergegeben werden, wenn ein Anwender Suchvorgänge ausführt. |
| `s:stream:chapter_name` | O | `ChapterInfo` | Der Anzeigename (für Menschen lesbar) des Kapitels. |
| `s:stream:chapter_id` | R | Medien-SDK | Die eindeutige ID des Kapitels. Dieser Wert wird automatisch anhand der folgenden Formel berechnet: `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | Der Index des Kapitels in der Kapitelliste (beginnend mit 1). |
| `l:stream:chapter_offset` | R | `ChapterInfo` | Der Versatz des Kapitels innerhalb des Hauptinhalts, ausschließlich Anzeigen. |
| `l:stream:chapter_length` | R | `ChapterInfo` | Die Dauer des Kapitels (in Sekunden ausgedrückt). |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | Anwenderspezifische Kapitelmetadaten. |

## Ereignisse zum Sitzungsende

| Name | erforderlich/optional | Datenquelle | Beschreibung   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | Medien-SDK | Der Name der Seite,`end``close` |

