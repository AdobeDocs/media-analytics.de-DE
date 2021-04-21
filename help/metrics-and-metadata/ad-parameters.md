---
title: Anzeigenparameter
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '1855'
ht-degree: 100%

---

# Anzeigenparameter {#ad-parameters}

In diesem Thema wird eine Liste von Videoanzeigendaten, einschließlich Kontextdatenwerten, vorgestellt, die Adobe über Lösungsvariablen sammelt.

Beschreibung der Tabellendaten:

* **Implementierung:** Angaben zu den Implementierungswerten und -anforderungen
   * *Schlüssel* - Variable, die entweder manuell in Ihrer App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich* - Gibt an, ob der Parameter für das allgemeine Video-Tracking erforderlich ist.
   * *Typ* - Gibt den Typ der festzulegenden Variablen an, nämlich Zeichenfolge oder Zahl.
   * *Gesendet mit* - Gibt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf beim Medienstart, *Ad Start* der Aufruf beim Anzeigenstart usw. *Close* ist der zusammengefasste Analytics-Aufruf, der am Ende der Mediensitzung oder am Ende der Anzeige, des Kapitels usw. vom Heartbeat-Server direkt an den Analytics-Server gesendet wird. Die Aufrufe zum Schließen sind in Netzwerk-Paketaufrufen nicht verfügbar.
   * *Min. SDK-Version* - Gibt an, welche SDK-Version Sie für den Zugriff auf den Parameter benötigen.
   * *Beispielwert* - Bietet ein Beispiel für die Verwendung häufiger Variablen.
* **Netzwerkparameter:** Zeigt die Werte an, die an Adobe Analytics- oder Heartbeat-Server übergeben werden. Diese Spalte enthält die Namen der Parameter, die in den von Adobe Media SDKs generierten Netzwerkaufrufen dargestellt werden.
* **Berichte:** Informationen zur Ansicht und Analyse der Videodaten.
   * *Verfügbar* - Zeigt an, ob die Daten standardmäßig im Reporting verfügbar sind (*Ja*) oder ob eine benutzerdefinierte Einrichtung erforderlich ist (*Benutzerdefiniert*).
   * *Reservierte Variable* - Gibt an, ob die Daten als Ereignis, eVar, prop oder Klassifizierung in einer reservierten Variablen erfasst werden.
   * *Berichtsname* - Name des Adobe Analytics-Berichts für eine Variable
   * *Kontextdaten* - Name der Adobe Analytics-Kontextdaten, die an den Reporting-Server übergeben und in Verarbeitungsregeln verwendet werden.
   * *Daten-Feed* - Spaltenname für eine Variable in Clickstream- oder Live-Stream-Daten-Feeds
   * *Audience Manager* - Trait Name in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändern Sie nicht die Klassifizierungsnamen für Variablen, die unter
>Reporting/Reservierte Variable als „Klassifizierung“ beschrieben sind.
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für das Medien-Tracking
>aktiviert ist. Adobe fügt von Zeit zu Zeit neue Eigenschaften hinzu. In diesem Fall müssen
>Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften
>zu erhalten. Während des Aktualisierungsvorgangs ermittelt Adobe
>anhand der Namen der Variablen, ob die Klassifizierungen aktiviert sind. Wenn eine
>fehlt, fügt Adobe die fehlenden erneut hinzu.

## Videoanzeigendaten {#ad-video-data}

### Anzeigen-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.id </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig  </li> <li> **Beispielwert:**<br/> „2125“ </li><li> **Beschreibung:**<br/> ID der Anzeige. (beliebige Integer- und/oder Buchstaben-Kombination)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Heartbeat:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> Bei BESUCH </li> <li> **Berichtsname:**<br/> Anzeige </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>name) </li> <li> **Daten-Feed:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Anzeigenposition innerhalb der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.podPosition </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/> Die Position (Index) der Anzeige innerhalb der übergeordneten Werbeunterbrechung. Die erste Anzeige weist den Index 0 auf, die zweite 1 usw.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Heartbeat:**<br/> (s:asset:pod_position) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> Anzeigenposition innerhalb der Werbeunterbrechung </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Daten-Feed:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Anzeigenlänge

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.length </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/> „15“  </li><li> **Beschreibung:**<br/> Länge der Videoanzeige in Sekunden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Heartbeat:**<br/> (l:asset:ad_length) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar und Klassifizierung </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> Anzeigenlänge und Anzeigenlänge (Variable) </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>length) </li> <li> **Daten-Feed:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Name des Anzeigenplayers

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.playerName </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „Freewheel“ </li><li> **Beschreibung:**<br/> Der Name des Players, der für das Rendering der Werbeanzeige verantwortlich ist.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> Name des Anzeigenplayers </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Daten-Feed:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Name der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.podFriendlyName </li> <li> **Erforderlich:**<br/> SDK: Ja; API: Nein. </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „pre-roll“ </li><li> **Beschreibung:**<br/> Der Anzeigename der Werbeunterbrechung.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:pod_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Klassifizierung </li> <li> **Berichtsname:**<br/> Name der Werbeunterbrechung </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Index der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.podPosition </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/> Der Index der Werbeunterbrechung innerhalb des Inhalts, beginnend bei 1. Diese Eigenschaft wird **nur** vom Medien-SDK verwendet, um die ID der Werbeunterbrechung zu generieren.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/> nein </li> <li> **Reservierte Variable:**<br/> nicht verfügbar </li> <li> **Berichtsname:**<br/> nicht verfügbar </li> <li> **Kontextdaten:**<br/> </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Position der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.podSecond </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 90 </li><li> **Beschreibung:**<br/> Der Offest der Werbeunterbrechung innerhalb des Inhalts in Sekunden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Heartbeat:**<br/> (l:asset:pod_offset) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Klassifizierung </li> <li> **Berichtsname:**<br/> Position der Werbeunterbrechung </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Heartbeat:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> Anzeigen-Pod </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>pod) </li> <li> **Daten-Feed:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Anzeigenname

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/> media.ad.name </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/> „Ford F-150“ </li><li> **Beschreibung:**<br/> Der Anzeigename der Werbeanzeige.  In Berichten stellt „Anzeigenname“ die Klassifizierung und „Anzeigenname (Variable)“ das eVar dar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:ad_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar und Klassifizierung </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> Anzeigenname und Anzeigenname (Variable) </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Standard-Anzeigenmetadaten {#standard-ad-metadata}

### Advertiser

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> ADVERTISER </li> <li> **API-Schlüssel:**<br/> media.ad.advertiser </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>  </li><li> **Beschreibung:**<br/> Das Unternehmen/die Marke des Produkts, das in der Anzeige vorgestellt wird.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> <i>Advertiser </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Daten-Feed:**<br/> videoadvertiser </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### Kampagnen-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> CAMPAIGN_ID </li> <li> **API-Schlüssel:**<br/> media.ad.campaignId </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> Integer oder Name (Zeichenfolge).  </li><li> **Beschreibung:**<br/> Die ID der Anzeigenkampagne.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>Kampagne) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> <i>Kampagnen-ID </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>Kampagne) </li> <li> **Daten-Feed:**<br/> videocampaign </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### Creative-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> CREATIVE_ID </li> <li> **API-Schlüssel:**<br/> media.ad.creativeId </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> Integer oder Name (Zeichenfolge).  </li><li> **Beschreibung:**<br/> ID des Anzeigenmotivs.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> <i>Creative-ID </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>creative) </li> <li> **Daten-Feed:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### Site-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> SITE_ID </li> <li> **API-Schlüssel:**<br/> media.ad.siteId </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>  </li><li> **Beschreibung:**<br/> ID der Anzeigen-Site.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>site) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Verwenden Sie eine benutzerdefinierte Verarbeitungsregel </i> </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>site) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### Creative-URL

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> CREATIVE_URL </li> <li> **API-Schlüssel:**<br/> media.ad.creativeURL </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>  </li><li> **Beschreibung:**<br/> URL des Anzeigenmotivs.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Verwenden Sie eine benutzerdefinierte Verarbeitungsregel </i> </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### Platzierungs-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> PLACEMENT_ID </li> <li> **API-Schlüssel:**<br/> media.ad.placementId </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>  </li><li> **Beschreibung:**<br/> Die Platzierungs-ID der Anzeige.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placement) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Verwenden Sie eine benutzerdefinierte Verarbeitungsregel </i> </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>placement) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Anzeigenmetriken {#ad-metrics}

### Werbung gestartet

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Start </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/> Die Anzahl der Videoanzeigenstarts.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>view) </li> <li> **Heartbeat:**<br/>  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Ereignis </li> <li> **Berichtsname:**<br/> Ad Starts </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>view) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Werbung beendet

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/> Die Anzahl der Anzeigenbeendigungen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Heartbeat:**<br/> (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Ereignis </li> <li> **Berichtsname:**<br/> Ad Closeen </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### Besuchszeit für Anzeige

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 15 </li><li> **Beschreibung:**<br/> Die insgesamt mit der Wiedergabe der Anzeige verbrachte Zeit in Sekunden (also die Anzahl der wiedergegebenen Sekunden).  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Daten-Feeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Ereignis </li> <li> **Berichtsname:**<br/> Besuchszeit für Anzeige </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Kontextdaten:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Verwandte APIs {#section_Related_APIs}

### createAdObject-APIs:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject-APIs:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig-APIs:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
