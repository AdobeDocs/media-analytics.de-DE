---
title: Beschreibungen der Heartbeat-Parameter
description: Untersuchen Sie die Heartbeat-Parameter, die Adobe auf dem Media Analytics-Server (Heartbeats) sammelt und verarbeitet.
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Streaming Media, Variables"
role: User, Admin, Data Engineer
source-git-commit: 70900e305c3ed7a2be4069c6f296d56f1f6e0966
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 99%

---

# Beschreibungen der Media Analytics (Heartbeat)-Parameter{#heartbeat-parameter-descriptions}

Liste der Media Analytics-Parameter, die Adobe erfasst und auf dem Media Analytics (Heartbeat)-Server verarbeitet:

## Alle Ereignisse

| Name | Datenquelle |  Beschreibung  |
| ---  | --- | --- |
| `s:event:type` | Medien-SDK | (Erforderlich)<br/><br/>Der Typ des zu verfolgenden Ereignisses. Ereignistypen: <ul> <li> s:event:type=start </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | Medien-SDK | (Erforderlich)<br/><br/>Der Zeitstempel des letzten Ereignisses mit demselben Typ in dieser Sitzung. Der Wert ist -1. |
| `l:event:ts` | Medien-SDK | (Erforderlich)<br/><br/>Der Zeitstempel des Ereignisses. |
| `l:event:duration` | Medien-SDK | (Erforderlich)<br/><br/>Der Wert wird intern (in Millisekunden) von dem Media SDK und nicht vom Player festgelegt. Er wird verwendet, um am Backend Metriken zur Besuchszeit zu berechnen. a.media.totalTimePlayed wird beispielsweise aus der Summe aller generierten Wiedergabe-Heartbeats (type=play) berechnet. <br/>*Hinweis:* Dieser Parameter ist bei bestimmten Ereignissen auf 0 gesetzt, da es sich um „Statusänderungsereignisse“ (z. B. type=complete, type=chapter_complete oder type=bitrate_change) handelt. |
| `l:event:playhead` | VideoInfo | (Erforderlich)<br/><br/>Die Abspielleiste befindet sich zum Zeitpunkt, zu dem das Ereignis aufgezeichnet wurde, im derzeit aktiven Asset (Hauptinhalt oder Anzeige). |
| `s:event:sid` | Medien-SDK | (Erforderlich)<br/><br/>Die Sitzungs-ID (eine zufällig generierte Zeichenfolge). Alle Ereignisse in einer bestimmten Sitzung (Video und Anzeigen) sollten gleich sein. |
| `l:asset:duration` / `l:asset:length` <br/> (von der Dauer in umbenannt) | VideoInfo | (Erforderlich)<br/><br/>Die Video-Asset-Länge des Haupt-Assets. |
| `s:asset:publisher` | MediaHeartbeatConfig | (Erforderlich)<br/><br/>Der Herausgeber des Assets. |
| `s:asset:video_id` | VideoInfo | (Erforderlich)<br/><br/>Eine ID, mit der das Video im Katalog des Herausgebers eindeutig identifiziert wird. |
| `s:asset:type` | Medien-SDK | (Erforderlich)<br/><br/>Der Asset-Typ (Hauptinhalt oder Anzeige). |
| `s:stream:type` | VideoInfo | (Erforderlich)<br/><br/>Der Stream-Typ. Kann einer der folgenden Werte sein: <ul> <li> live </li> <li> vod </li> <li> „Lineare Zuordnung“ </li> </ul> |
| `s:user:id` | Konfigurationsobjekt für mobile App Measurement-VisitorID | (Optional)<br/><br/>Speziell festgelegte Besucher-ID des Benutzers. |
| `s:user:aid` | Experience Cloud-Organisation | (Optional)<br/><br/>Der Analytics-Besucher-ID-Wert des Benutzers. |
| `s:user:mid` | Experience Cloud-Organisation | (Erforderlich)<br/><br/>Der Experience Cloud-Besucher-ID-Wert des Benutzers. |
| `s:cuser:customer_user_ids_x` | MediaHeartbeatConfig | (Optional)<br/><br/>Alle in Audience Manager festgelegten Kundenbenutzer-IDs. |
| `l:aam:loc_hint` | MediaHeartbeatConfig | (Erforderlich)<br/><br/>AAM-Daten, die bei jeder Nutzlast nach aa_start gesendet werden |
| `s:aam:blob` | MediaHeartbeatConfig | (Erforderlich)<br/><br/>AAM-Daten, die bei jeder Nutzlast nach aa_start gesendet werden |
| `s:sc:rsid` | Report Suite-ID (oder -IDs) | (Erforderlich)<br/><br/>Adobe Analytics-RSID, an die Berichte gesendet werden sollen. |
| `s:sc:tracking_server` | MediaHeartbeatConfig | (Erforderlich)<br/><br/>Adobe Analytics-Tracking-Server. |
| `h:sc:ssl` | MediaHeartbeatConfig | (Erforderlich)<br/><br/>Gibt an, ob der Traffic über HTTPS (bei 1) oder HTTP (bei 0) erfolgt. |
| `s:sp:ovp` | MediaHeartbeatConfig | (Optional)<br/><br/>Legen Sie bei Primetime-Playern „primetime“ und bei anderen Playern den tatsächlichen OVP fest. |
| `s:sp:sdk` | MediaHeartbeatConfig | (Erforderlich)<br/><br/>Die OVP-Versionszeichenfolge. |
| `s:sp:player_name` | VideoInfo | (Erforderlich)<br/><br/>Videoplayername (die tatsächliche Player-Software, mit der der Player identifiziert wird). |
| `s:sp:channel` | MediaHeartbeatConfig | (Optional)<br/><br/>Der Kanal, auf dem der Benutzer den Inhalt betrachtet. Bei einer mobilen App den App-Namen. Bei einer Website den Domänennamen. |
| `s:sp:hb_version` | Medien-SDK | (Erforderlich)<br/><br/>Die Versionsnummer der Media SDK-Bibliothek, die den Aufruf ausgibt. |
| `l:stream:bitrate` | QoSInfo | (Erforderlich)<br/><br/>Der aktuelle Wert der Stream-Bitrate (in bps). |

## Fehlerereignisse

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| `s:event:source` | Medien-SDK | (Erforderlich)<br/><br/>Die Quelle des Fehlers (entweder intern im Player oder auf Anwendungsebene). |
| `s:event:id` | Medien-SDK | (Erforderlich)<br/><br/>Fehler-ID, mit der der Fehler eindeutig identifiziert wird. |

## Anzeigenereignisse

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| `s:asset:ad_id` | AdInfo | (Erforderlich)<br/><br/>Der Name der Anzeige. |
| `s:asset:ad_sid` | Medien-SDK | (Erforderlich)<br/><br/>Eine eindeutige ID, die vom Media SDK generiert und an alle anzeigenbezogenen Pings angehängt wird. |
| `s:asset:pod_id` | Medien-SDK | (Erforderlich)<br/><br/>Werbeunterbrechungs-ID im Video. Dieser Wert wird automatisch anhand der folgenden Formel berechnet: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| `s:asset:pod_position` | AdBreakInfo | (Erforderlich)<br/><br/>Index der Anzeige innerhalb der Werbeunterbrechung (die erste Anzeige hat den Index 0, die zweite Anzeige den Index 1 usw.). |
| `s:asset:resolver` | AdBreakInfo | (Erforderlich)<br/><br/>Der Anzeigenauflöser. |
| `s:meta:custom_ad_metadata.x` | MediaHeartbeat | (Optional)<br/><br/>Die benutzerdefinierten Anzeigenmetadaten. |

## Kapitelereignisse

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| `s:stream:chapter_sid` | Medien-SDK | (Erforderlich)<br/><br/>Die eindeutige ID, die mit der Wiedergabeinstanz des Kapitels verknüpft ist. <br/> **Hinweis:** Ein Kapitel kann mehrmals wiedergegeben werden, wenn ein Anwender Suchvorgänge ausführt. |
| `s:stream:chapter_name` | ChapterInfo | (Optional)<br/><br/>Der Anzeigename (für Menschen lesbar) des Kapitels. |
| `s:stream:chapter_id` | Medien-SDK | (Erforderlich)<br/><br/>Die eindeutige ID des Kapitels. Dieser Wert wird automatisch anhand der folgenden Formel berechnet: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| `l:stream:chapter_pos` | ChapterInfo | (Erforderlich)<br/><br/>Der Index des Kapitels in der Kapitelliste (beginnend mit 1). |
| `l:stream:chapter_offset` | ChapterInfo | (Erforderlich)<br/><br/>Der Offset des Kapitels innerhalb des Hauptinhalts ohne Anzeigen. |
| `l:stream:chapter_length` | ChapterInfo | (Erforderlich)<br/><br/>Die Dauer des Kapitels (in Sekunden ausgedrückt). |
| `s:meta:custom_chapter_metadata.x` | ChapterInfo | (Optional)<br/><br/>Benutzerdefinierte Kapitelmetadaten. |

## Ereignisse zum Sitzungsende

| Name | Datenquelle | Beschreibung   |
| ---  | --- | --- |
| `s:event:type=end` | Medien-SDK | (Erforderlich)<br/><br/> Der Wert `end` `close` |
