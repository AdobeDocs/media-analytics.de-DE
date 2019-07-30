---
seo-title: Kapitelparameter
title: Kapitelparameter
uuid: 2 a 6 b 9247-a 694-46 e 9-98 e 1-424 c 08 c 27 ec 2
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Kapitelparameter{#chapter-parameters}

Dieses Thema enthält eine Liste von Kapitel- und/oder Segmentdaten, einschließlich Kontextdatenwerten, die Adobe über Lösungsvariablen sammelt.

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

## Kapitelmetadaten {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### Kapitelname

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/>media.chapter.friendlyName </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Kapitelstart, Kapitelschließung </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> " The Big Bang Chapter 2 - Dating " </li><li> **Beschreibung:**<br/>Der Name des Kapitels und/oder Segments.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>Friendlyname) </li> <li> **Heartbeat:**<br/> (s: stream: chapter_ name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Wird standardmäßig erstellt.  </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Kapitelname </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>Friendlyname) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>Friendlyname) </li> </ul> |

### Kapitelposition

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/>media.chapter.index </li> <li> **Erforderlich:**<br/> SDK: Nein; API: Ja. </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Kapitelschließen </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> 2 </li><li> **Beschreibung:**<br/>Die Position (Index, Ganzzahl) des Kapitels innerhalb des Inhalts.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (l: stream: chapter_ pos) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Kapitelposition </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>position) </li> <li> **Datenfeed:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>position) </li> </ul> |

### Kapiteloffset

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/>media.chapter.offset </li> <li> **Erforderlich:**<br/> SDK: Nein; API: Ja. </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Kapitelschließen </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> 58 </li><li> **Beschreibung:**<br/>Der Offset des Kapitels innerhalb des Inhalts (in Sekunden) von Anfang an.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>offset) </li> <li> **Heartbeat:**<br/> (l: stream: chapter_ offset) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Kapiteloffset </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>offset) </li> <li> **Datenfeed:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>offset) </li> </ul> |

### Kapitellänge

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.chapter.length </li> <li> **Erforderlich:**<br/> SDK: Nein; API: Ja. </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Kapitelschließen </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> 486 </li><li> **Beschreibung:**<br/>Die Länge des Kapitels in Sekunden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>length) </li> <li> **Heartbeat:**<br/> (l: stream: chapter_ length) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Kapitellänge </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>length) </li> <li> **Datenfeed:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>length) </li> </ul> |

### Kapitel

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Kapitelschließen </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die automatisch generierte ID des Kapitels.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (s: stream: chapter_ id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Kapitel </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>name) </li> <li> **Datenfeed:**<br/>videochapter </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>name) </li> </ul> |

## Kapitelmetriken {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### Chapter Start

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt  </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/>Chapter Start </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Kapitelstarts. **Wichtig:** Wenn dieses Ereignis festgelegt wurde, lautet der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = chapter_ start) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> Kapitelstarts G </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>view) </li> <li> **Datenfeed:**<br/>videochapterstart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>view) </li> </ul> |

### Kapitelbeendigung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt  </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Kapitelschließen </li> <li> **Min. SDK-Version:** 1.3</li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Kapitelbeendigungen. **Wichtig:** Wenn dieses Ereignis festgelegt wurde, lautet der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>complete) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = chapter_ complete) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> Kapitelbeendigungen G </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>complete) </li> <li> **Datenfeed:**<br/>videochaptercomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>complete) </li> </ul> |

### Besuchszeit für Kapitel

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt  </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Kapitelschließen </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die im Kapitel verbrachte Zeit. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>Timeplayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> Kapitelbesuchszeit G </li> <li> **Kontextdaten:**<br/> (a. media. chapter.<br/>Timeplayed) </li> <li> **Datenfeed:**<br/>videochaptertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>Timeplayed) </li> </ul> |

## Related APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
