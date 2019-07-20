---
seo-title: Anzeigenparameter
title: Anzeigenparameter
uuid: 92 cd 7 f 97-bb 5 a -4 de 6-8946-453 d 30271 d 0 f
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# Anzeigenparameter{#ad-parameters}

In diesem Thema wird eine Liste von Videoanzeigendaten, einschließlich Kontextdatenwerten, vorgestellt, die Adobe über Lösungsvariablen sammelt.

Beschreibung der Tabellendaten:

* **Implementierung:** Informationen zu Implementierungswerten und -anforderungen.
   * *Schlüssel:* Variable, die entweder manuell in der App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich:* Gibt an, ob der Parameter für das Basis-Video-Tracking erforderlich ist.
   * *Typ:* Gibt den Typ der Variablen (Zeichenfolge oder Zahl) an.
   * *Gesendet Mit* : Zeigt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf, der beim Medienstart gesendet wird, *Anzeigenstart* ist der Analytics-Aufruf, der beim Anzeigenstart gesendet wird usw. *Die Aufrufe schließen* sind die kompilierten Analyseaufrufe, die direkt vom Heartbeat-Server an den Analytics-Server am Ende der Mediensitzung oder am Ende der Anzeige, Kapitel usw. gesendet werden. Die Schließen-Aufrufe sind in Netzwerkpaketaufrufen nicht verfügbar.
   * *Min. SDK-Version:* Gibt die SDK-Version an, die Sie benötigen, um auf den Parameter zuzugreifen.
   * *Beispielwert:* Bietet ein Beispiel für häufige Variablenverwendung.
* **Netzwerkparameter:** Zeigt die Werte an, die an Adobe Analytics- oder Heartbeat-Server übergeben werden. Diese Spalte enthält die Namen der Parameter, die in von Adobe Media SDKs generierten Netzwerkaufrufen enthalten sind.
* **Reporting:** Informationen zur Anzeige und Analyse der Videodaten.
   * *Verfügbar:* Gibt an, ob die Daten standardmäßig in Berichten verfügbar sind (*Ja*) oder manuell eingerichtet werden müssen (*Anwenderspezifisch*).
   * *Reservierte Variablen:* Gibt an, ob die Daten als Ereignis, eVar, Prop oder Classification in einer reservierten Variablen erfasst werden.
   * *Berichtsname:* Name des Adobe Analytics-Berichts für die Variable.
   * *Kontextdaten:* Name der Adobe Analytics-Kontextdaten, die an den Reporting-Server übergeben und in Verarbeitungsregeln verwendet werden.
   * *Datenfeed:* Spaltenname für die Variable in Clickstream- oder Live-Stream-Datenfeeds
   * *Audience Manager:* Eigenschaftsname in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändern Sie nicht die Classification-Namen für die unten aufgeführten Variablen, die unter Berichterstellung/Reservierte Variable als "Classification" beschrieben werden.\
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für die Medienverfolgung aktiviert ist. Von Zeit zu Zeit fügt Adobe neue Eigenschaften hinzu. Falls dies eintritt, müssen Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften zu erhalten. Während des Aktualisierungsprozesses bestimmt Adobe, ob die Klassifizierungen durch Überprüfen der Namen der Variablen aktiviert werden. Wenn eine davon fehlt, fügt Adobe die fehlenden Felder wieder hinzu.

## Videoanzeigendaten {#section_hq3_nbv_51b}

### Anzeigen-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.id </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig  </li> <li> **Beispielwert:**<br/> " 2125 " </li><li> **Beschreibung:**<br/>ID der Anzeige. (beliebige Integer- und/oder Buchstaben-Kombination)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.na me) </li> <li> **Heartbeat:**<br/> (s: Asset: ad_ id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Anzeige </li> <li> **Kontextdaten:**<br/> (a.media.ad.na me) </li> <li> **Datenfeed:**<br/>videoad </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.name) </li> </ul> |



### Anzeigenposition innerhalb der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podPosition </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Position (Index) der Anzeige innerhalb der übergeordneten Werbeunterbrechung. Die erste Anzeige weist den Index 0 auf, die zweite 1 usw.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dposition) </li> <li> **Heartbeat:**<br/> (s: Asset: pod_ position) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigenposition innerhalb der Werbeunterbrechung </li> <li> **Kontextdaten:**<br/> (a.media.ad.po Dposition) </li> <li> **Datenfeed:**<br/>videoadinpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Anzeigenlänge

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.length </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/> " 15 «  </li><li> **Beschreibung:**<br/>Länge der Videoanzeige in Sekunden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.le ngth) </li> <li> **Heartbeat:**<br/> (l: Asset: ad_ length) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar und Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigenlänge und Anzeigenlänge (Variable) </li> <li> **Kontextdaten:**<br/> (a.media.ad.le ngth) </li> <li> **Datenfeed:**<br/>videoadlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.length) </li> </ul> |



### Name des Anzeigenplayers

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.playerName </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> " Freewheel « </li><li> **Beschreibung:**<br/>Der Name des Players, der für die Anzeige der Anzeige verantwortlich ist.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.pl Ayername) </li> <li> **Heartbeat:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Name des Anzeigenplayers </li> <li> **Kontextdaten:**<br/> (a.media.ad.pl Ayername) </li> <li> **Datenfeed:**<br/>videoadplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Name der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podFriendlyName </li> <li> **Erforderlich:**<br/> SDK: Ja; API: Nein. </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> " pre-roll " </li><li> **Beschreibung:**<br/>Der Anzeigename der Werbeunterbrechung.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **Heartbeat:**<br/> (s: Asset: pod_ name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Name der Werbeunterbrechung </li> <li> **Kontextdaten:**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **Datenfeed:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Index der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podPosition </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Der Index der Werbeunterbrechung innerhalb des Inhalts, der mit 1 beginnt. Diese Eigenschaft wird **nur** vom Medien-SDK verwendet, um die ID der Werbeunterbrechung zu generieren.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/>nein </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> </li> <li> **Datenfeed:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Position der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podSecond </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 90 </li><li> **Beschreibung:**<br/>Der Offset der Werbeunterbrechung innerhalb des Inhalts in Sekunden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dsecond) </li> <li> **Heartbeat:**<br/> (l: Asset: pod_ offset) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Position der Werbeunterbrechung </li> <li> **Kontextdaten:**<br/> (a.media.ad.po Dsecond) </li> <li> **Datenfeed:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> c 4 a 777424 c 84067899 b 807 c 76722 d 495_ 1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po d) </li> <li> **Heartbeat:**<br/> (l: Asset: pod_ id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigen-Pod </li> <li> **Kontextdaten:**<br/> (a.media.ad.po d) </li> <li> **Datenfeed:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Anzeigenname

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.name </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/> " Ford F -150 " </li><li> **Beschreibung:**<br/>Anzeigename der Anzeige. In Berichten stellt „Anzeigenname“ die Classification und „Anzeigenname (Variable)“ die eVar dar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.fr Iendlyname) </li> <li> **Heartbeat:**<br/> (s: Asset: ad_ name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar und Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigenname und Anzeigenname (Variable) </li> <li> **Kontextdaten:**<br/> (a.media.ad.fr Iendlyname) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Standard-Anzeigenmetadaten {#section_EFB805867916411E84DE1BA5A183D86A}

### Advertiser

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ADVERTISER </li> <li> **API-Schlüssel:**<br/>media.ad.advertiser </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Unternehmen/Marke, deren Produkt in der Anzeige hervorgehoben wird.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ad vertiser) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ad vertiser) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i>Advertiser </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.ad vertiser) </li> <li> **Datenfeed:**<br/>videoadvertiser </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### Kampagnen-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>CAMPAIGN_ID </li> <li> **API-Schlüssel:**<br/>media.ad.campaignId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> Ganzzahl oder Name (Zeichenfolge).  </li><li> **Beschreibung:**<br/>ID der Werbekampagne.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ca mpaign) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ca mpaign) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i>Kampagnen-ID </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.ca mpaign) </li> <li> **Datenfeed:**<br/>videocampaign </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### Creative-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>CREATIVE_ID </li> <li> **API-Schlüssel:**<br/>media.ad.creativeId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> Ganzzahl oder Name (Zeichenfolge).  </li><li> **Beschreibung:**<br/>ID der Werbeanzeige.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.cr eative) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr eative) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i>Creative-ID </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.cr eative) </li> <li> **Datenfeed:**<br/>adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creative) </li> </ul> |



### Site-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SITE_ID </li> <li> **API-Schlüssel:**<br/>media.ad.siteId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>ID der Werbeanzeige.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.si te) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.si te) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Benutzerdefinierte Verarbeitungsregel verwenden </i> </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i> </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.si te) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.site) </li> </ul> |



### Creative-URL

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>CREATIVE_URL </li> <li> **API-Schlüssel:**<br/>media.ad.creativeURL </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>URL der kreativen Werbeunterbrechung.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.cr Eativeurl) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr Eativeurl) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Benutzerdefinierte Verarbeitungsregel verwenden </i> </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i> </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.cr Eativeurl) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### Platzierungs-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>PLACEMENT_ID </li> <li> **API-Schlüssel:**<br/>media.ad.placementId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Platzierungs-ID der Anzeige.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.pl acement) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.pl acement) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Benutzerdefinierte Verarbeitungsregel verwenden </i> </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i> </i> </li> <li> **Kontextdaten:**<br/> (a.media.ad.pl acement) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Anzeigenmetriken {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### Werbung gestartet

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Anzahl der Videoanzeigenstarts.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.vi ew) </li> <li> **Heartbeat:**<br/> (s: Ereignis: type = start)<br/> (s: Asset: type = ad) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Anzeigenstarts </li> <li> **Datenfeed:**<br/>videoadstart </li> <li> **Kontextdaten:**<br/> (a.media.ad.vi ew) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.view) </li> </ul> |



### Werbung beendet

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Anzahl der Videoanzeigenbeendigungen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.com plete) </li> <li> **Heartbeat:**<br/> (s: Ereignis: type = complete)<br/> (s: Asset: type = ad)  </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Anzeigenbeendigungen </li> <li> **Datenfeed:**<br/>videoadcomplete </li> <li> **Kontextdaten:**<br/> (a.media.ad.com plete) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.complete) </li> </ul> |



### Besuchszeit für Anzeige

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 15 </li><li> **Beschreibung:**<br/>Die Gesamtdauer der Anzeige in Sekunden (d. h. die Anzahl der wiedergegebenen Sekunden). Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ti Meplayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Besuchszeit für Anzeige </li> <li> **Datenfeed:**<br/>videoadtime </li> <li> **Kontextdaten:**<br/> (a.media.ad.ti Meplayed) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### Createadobject-apis:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### Createadbreakobject-apis:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### Mediaheartbeatconfig apis:

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

