---
seo-title: Anzeigenparameter
title: Anzeigenparameter
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: 4a14e2faae6401a3f885eb5e341c1344d7f1e94d

---


# Anzeigenparameter{#ad-parameters}

In diesem Thema wird eine Liste von Videoanzeigendaten, einschließlich Kontextdatenwerten, vorgestellt, die Adobe über Lösungsvariablen sammelt.

Beschreibung der Tabellendaten:

* **Implementierung:** Informationen zu Implementierungswerten und -anforderungen.
   * *Schlüssel:* Variable, die entweder manuell in der App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich:* Gibt an, ob der Parameter für das Basis-Video-Tracking erforderlich ist.
   * *Typ:* Gibt den Typ der Variablen (Zeichenfolge oder Zahl) an.
   * *Gesendet mit* - Gibt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf, der beim Medienstart gesendet wird, *Ad Start* ist der Analytics-Aufruf, der beim Anzeigenstart gesendet wird usw.; Die *Close* -Aufrufe sind die kompilierten Analytics-Aufrufe, die direkt vom Heartbeat-Server an den Analytics-Server am Ende der Mediensitzung oder am Ende der Anzeige, des Kapitels usw. gesendet werden. Die close-Aufrufe sind nicht in Netzwerkpaketaufrufen verfügbar.
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
>Ändern Sie die Classification-Namen für die unten aufgeführten Variablen nicht
>beschrieben unter Berichterstellung/Reservierte Variable als "Classification".
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für Medien aktiviert wird
>Verfolgung. Von Zeit zu Zeit fügt Adobe neue Eigenschaften hinzu und, wenn dies auftritt,
>Kunden müssen ihre Report Suites erneut aktivieren, um Zugriff auf neue Medien zu erhalten
>Eigenschaften. Während des Aktualisierungsvorgangs bestimmt Adobe, ob die Variable
>Klassifizierungen werden aktiviert, indem die Namen der Variablen überprüft werden. Falls einer von
>fehlen, fügt Adobe die fehlenden erneut hinzu.

## Videoanzeigendaten {#section_hq3_nbv_51b}

### Anzeigen-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.id </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig  </li> <li> ****<br/> Beispielwert: "2125" </li><li> **Beschreibung:**<br/>ID der Anzeige. (beliebige Integer- und/oder Buchstaben-Kombination)  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>name) </li> <li> ****<br/> Heartbeat: (s:asset:ad_id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Anzeige </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>name) </li> <li> **Datenfeed:**<br/>videoad </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Anzeigenposition innerhalb der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podPosition </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 1 </li><li> **Beschreibung:**<br/>Die Position (Index) der Anzeige innerhalb der übergeordneten Werbeunterbrechung. Die erste Anzeige weist den Index 0 auf, die zweite 1 usw.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>podPosition) </li> <li> ****<br/> Heartbeat: (s:asset:pod_position) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigenposition innerhalb der Werbeunterbrechung </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>podPosition) </li> <li> **Datenfeed:**<br/>videoadinpod </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Anzeigenlänge

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.length </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> ****<br/> Beispielwert: "15"  </li><li> **Beschreibung:**<br/>Länge der Videoanzeige in Sekunden   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>length) </li> <li> ****<br/> Heartbeat: (l:asset:ad_length) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar und Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigenlänge und Anzeigenlänge (Variable) </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>length) </li> <li> **Datenfeed:**<br/>videoadlength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Name des Anzeigenplayers

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.playerName </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: "Freiluftfahrzeug" </li><li> **Beschreibung:**<br/>Der Name des Players, der für die Wiedergabe der Anzeige verantwortlich ist.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>playerName) </li> <li> ****<br/> Heartbeat: (s:sp:player_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Name des Anzeigenplayers </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>playerName) </li> <li> **Datenfeed:**<br/>videoadplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Name der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podFriendlyName </li> <li> ****<br/> Erforderlich: SDK: Ja; API: Anzahl </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: "Pre-Roll" </li><li> **Beschreibung:**<br/>Der Anzeigenumbruch.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>podFriendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:pod_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Name der Werbeunterbrechung </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>podFriendlyName) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Index der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podPosition </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 1 </li><li> **Beschreibung:**<br/>Der Index der Werbeunterbrechung im Inhalt, beginnend mit 1. Diese Eigenschaft wird **nur** vom Medien-SDK verwendet, um die ID der Werbeunterbrechung zu generieren.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/>nein </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Position der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.podSecond </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 90 </li><li> **Beschreibung:**<br/>Der Versatz der Werbeunterbrechung im Inhalt in Sekunden.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>podSecond) </li> <li> ****<br/> Heartbeat: (l:asset:pod_offset) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Position der Werbeunterbrechung </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>podSecond) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID der Werbeunterbrechung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>pod) </li> <li> ****<br/> Heartbeat: (s:asset:pod_id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigen-Pod </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>pod) </li> <li> **Datenfeed:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Anzeigenname

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-Schlüssel:**<br/>media.ad.name </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> ****<br/> Beispielwert: "Ford F-150" </li><li> **Beschreibung:**<br/>Anzeigenname.  In Berichten stellt „Anzeigenname“ die Classification und „Anzeigenname (Variable)“ die eVar dar.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>friendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:ad_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar und Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Anzeigenname und Anzeigenname (Variable) </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>friendlyName) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Standard-Anzeigenmetadaten {#section_EFB805867916411E84DE1BA5A183D86A}

### Advertiser

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ADVERTISER </li> <li> **API-Schlüssel:**<br/>media.ad.advertiser </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Firma/Marke, deren Produkt in der Anzeige vorgestellt wird.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>advertiser) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i>Advertiser </i> </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>advertiser) </li> <li> **Datenfeed:**<br/>videoadvertiser </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### Kampagnen-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>CAMPAIGN_ID </li> <li> **API-Schlüssel:**<br/>media.ad.campaignId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: Ganzzahl oder Name (Zeichenfolge).  </li><li> **Beschreibung:**<br/>ID der Werbekampagne.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>Kampagne) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.cacampaign) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i>Kampagnen-ID </i> </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>Kampagne) </li> <li> **Datenfeed:**<br/>videocampaign </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### Creative-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>CREATIVE_ID </li> <li> **API-Schlüssel:**<br/>media.ad.creativeId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: Ganzzahl oder Name (Zeichenfolge).  </li><li> **Beschreibung:**<br/>ID des Werbekreativen.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>creative) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i>Creative-ID </i> </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>creative) </li> <li> **Datenfeed:**<br/>adclassificationcreative </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### Site-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SITE_ID </li> <li> **API-Schlüssel:**<br/>media.ad.siteId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>ID der Anzeigen-Site.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>Site vor) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Benutzerdefinierte Verarbeitungsregel verwenden </i> </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i> </i> </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>Site vor) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### Creative-URL

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>CREATIVE_URL </li> <li> **API-Schlüssel:**<br/>media.ad.creativeURL </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>URL des Werbekreativen.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>creativeURL) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Benutzerdefinierte Verarbeitungsregel verwenden </i> </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i> </i> </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>creativeURL) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### Platzierungs-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>PLACEMENT_ID </li> <li> **API-Schlüssel:**<br/>media.ad.placementId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start, Ad Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Platzierungs-ID der Anzeige.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>placement) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Verfügbar:**<br/> <i>Benutzerdefinierte Verarbeitungsregel verwenden </i> </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> <i> </i> </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>placement) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Anzeigenmetriken {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### Werbung gestartet

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Start </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: TRUE </li><li> **Beschreibung:**<br/>Anzahl der Videoanzeigenstarts.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>view) </li> <li> ****<br/> Heartbeat:  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Anzeigenstarts </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>view) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Werbung beendet

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: TRUE </li><li> **Beschreibung:**<br/>Anzahl der Videoanzeigen abgeschlossen.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>complete) </li> <li> ****<br/> Heartbeat: (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Anzeigenbeendigungen </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>complete) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### Besuchszeit für Anzeige

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Ad Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 15 </li><li> **Beschreibung:**<br/>Die Gesamtdauer der Anzeige in Sekunden (d. h. die Anzahl der abgespielten Sekunden).  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad)<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Besuchszeit für Anzeige </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Kontextdaten: (a.media.ad)<br/>timePlayed) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



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

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

