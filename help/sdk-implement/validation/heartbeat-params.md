---
seo-title: Beschreibungen der Heartbeat-Parameter
title: Beschreibungen der Heartbeat-Parameter
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
translation-type: tm+mt
source-git-commit: 10a5d921953339bef1cde2f802eb9ce0cb1bbe4b

---


# Beschreibungen der Media Analytics-Parameter (Heartbeats){#heartbeat-parameter-descriptions}

Liste der Media Analytics-Parameter, die Adobe auf dem Media Analytics-Server (Heartbeats) erfasst und verarbeitet:

## Alle Ereignisse

| Name | Datenquelle |  Beschreibung  |
| ---  | --- | --- |
| s:event:type | Medien-SDK | (Required)<br/><br/>The type of the event being tracked. Ereignistypen: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Medien-SDK | (Required)<br/><br/>The timestamp of the last event of the same type in this session. Der Wert ist -1. |
| l:event:ts | Medien-SDK | (Required)<br/><br/>The timestamp of the event. |
| l:event:duration | Medien-SDK | (Required)<br/><br/>This value is set internally (in milliseconds) by the Media SDK, not by the player. Er wird verwendet, um am Backend Metriken zur Besuchszeit zu berechnen. Beispiel: a.media.totalTimePlayed wird als Summe der Dauer aller generierten Play-Heartbeats (type=play) berechnet. <br/>** Hinweis: Dieser Parameter ist bei bestimmten Ereignissen auf 0 gesetzt, da es sich um "Statusänderungsereignisse"(z. B. type=complete, type=chapter_complete oder type=bitrate_change) handelt. |
| l:event:playhead | VideoInfo | (Required)<br/><br/>The playhead was inside the currently active asset (main or ad), when the event was recorded. |
| s:event:sid | Medien-SDK | (Required)<br/><br/>The session ID (a randomly generated string). Alle Ereignisse in einer bestimmten Sitzung (Video und Anzeigen) sollten gleich sein. |
| l:asset:duration / l:asset:length <br/>(Umbenannt von der Dauer) | VideoInfo | (Required)<br/><br/>The video asset length of the main asset. |
| s:asset:publisher | MediaHeartbeatConfig | (Required)<br/><br/>The publisher of the asset. |
| s:asset:video_id | VideoInfo | (Required)<br/><br/>An ID uniquely identifying the video in the publisher's catalog. |
| s:asset:type | Medien-SDK | (Required)<br/><br/>The asset type (main or ad). |
| s:stream:type | VideoInfo | (Erforderlich)<br/><br/>Der Stream-Typ. Kann einer der folgenden sein: <ul> <li> live </li> <li> vod </li> <li> „Lineare Zuordnung“ </li> </ul> |
| s:user:id | Konfigurationsobjekt für mobile App Measurement-VisitorID | (Optional)<br/><br/>User's specifically set Visitor ID. |
| s:user:aid | Experience Cloud-Organisation | (Optional)<br/><br/>The user's Analytics Visitor ID value. |
| s:user:mid | Experience Cloud-Organisation | (Required)<br/><br/>The user's Experience cloud visitor ID value. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Optional)<br/><br/>All customer user IDs set on Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:aam:blob | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:sc:rsid | Report Suite-ID (oder -IDs) | (Erforderlich)<br/><br/>Adobe Analytics-RSID, an die Berichte gesendet werden sollen. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Erforderlich)<br/><br/>Adobe Analytics-Tracking-Server. |
| h:sc:ssl | MediaHeartbeatConfig | (Required)<br/><br/>Whether the traffic is over HTTPS (if set to 1) or over HTTP (is set to 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Optional)<br/><br/>Set to "primetime" for Primetime players, or the actual OVP for other players. |
| s:sp:sdk | MediaHeartbeatConfig | (Required)<br/><br/>The OVP version string. |
| s:sp:player_name | VideoInfo | (Required)<br/><br/>Video player name (the actual player software, used to identify the player). |
| s:sp:channel | MediaHeartbeatConfig | (Optional)<br/><br/>The channel where the user is watching the content. Bei einer mobilen App ist dies der App-Name. Bei einer Website ist es der Domänenname. |
| s:sp:hb_version | Medien-SDK | (Erforderlich)<br/><br/>Die Versionsnummer der Media SDK-Bibliothek, die den Aufruf ausgibt. |
| l:stream:bitrate | QoSInfo | (Required)<br/><br/>The current value of the stream bitrate (in bps). |

## Fehlerereignisse

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| s:event:source | Medien-SDK | (Required)<br/><br/>The source of the error, either player-internal, or the application-level. |
| s:event:id | Medien-SDK | (Required)<br/><br/>Error ID, uniquely identifies the error. |

## Anzeigenereignisse

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Erforderlich)<br/><br/>Der Name der Anzeige. |
| s:asset:ad_sid | Medien-SDK | (Required)<br/><br/>A unique identifier generated by the Media SDK, appended to all ad-related pings. |
| s:asset:pod_id | Medien-SDK | (Required)<br/><br/>Pod ID inside the video. Dieser Wert wird automatisch anhand der folgenden Formel berechnet: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Required)<br/><br/>Index of the ad inside the pod (the first ad has index 0, the second ad has index 1, etc.). |
| s:asset:resolver | AdBreakInfo | (Erforderlich)<br/><br/>Der Anzeigenauflöser. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Optional)<br/><br/>The custom ad metadata. |

## Kapitelereignisse

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| s:stream:chapter_sid | Medien-SDK | (Required)<br/><br/>The unique identifier associated to the playback instance of the chapter.  <br/> **Hinweis:** Ein Kapitel kann mehrmals wiedergegeben werden, wenn ein Anwender Suchvorgänge ausführt. |
| s:stream:chapter_name | ChapterInfo | (Optional)<br/><br/>The chapter's friendly (i.e., human readable) name. |
| s:stream:chapter_id | Medien-SDK | (Required)<br/><br/>The unique ID of the chapter. Dieser Wert wird automatisch anhand der folgenden Formel berechnet: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:chapter_pos | ChapterInfo | (Required)<br/><br/>The chapter's index in the list of chapters (starting with 1). |
| l:stream:chapter_offset | ChapterInfo | (Required)<br/><br/>The chapter's offset (expressed in seconds) inside the main content, excluding ads. |
| l:stream:chapter_length | ChapterInfo | (Required)<br/><br/>The chapter's duration (expressed in seconds). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Optional)<br/><br/>Benutzerdefinierte Kapitelmetadaten. |

## Ereignisse zum Sitzungsende

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| s:event:type=end | Medien-SDK | (Erforderlich)<br/><br/> Die `end``close` |

