---
title: Kapitelparameter
description: „Erfahren Sie mehr über Kapitelparameter für Implementierung, Netzwerk und Reporting.“
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7e5ce452a9c96c4e34150ae0e06d73b0cff98741
workflow-type: ht
source-wordcount: '1169'
ht-degree: 100%

---

# Kapitelparameter {#chapter-parameters}

Dieses Thema enthält eine Liste von Kapitel- und/oder Segmentdaten, einschließlich Kontextdatenwerten, die Adobe über Lösungsvariablen sammelt.

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
   * *Audience Manager* - Trait Name in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändern Sie nicht die Classification-Namen für Variablen, die unter Berichterstellung/Reservierte Variable als „Classification“ beschrieben sind.\
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für das Medien-Tracking aktiviert ist. Adobe fügt von Zeit zu Zeit neue Eigenschaften hinzu. In diesem Fall müssen Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften zu erhalten. Während des Aktualisierungsvorgangs ermittelt Adobe anhand der Namen der Variablen, ob die Classifications aktiviert sind. Wenn eine fehlt, fügt Adobe die fehlenden erneut hinzu.

## Kapitelmetadaten {#chapter-metadata}

### Kapitelname

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/> media.chapter.friendlyName </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Chapter Start, Chapter Close </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> „The Big Bang Chapter 2 – Dating“ </li><li> **Beschreibung:**<br/> Der Name des Kapitels und/oder Segments.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/> Wird standardmäßig erstellt.  </li> <li> **Reservierte Variable:**<br/> Classification </li> <li> **Berichtsname:**<br/> Kapitelname </li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.dc:title </li> <li> **XDM-Feldpfad für Sammlung:**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### Kapitelposition

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/> media.chapter.index </li> <li> **Erforderlich:**<br/> SDK: Nein; API: Ja. </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> Chapter Close </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> 2 </li><li> **Beschreibung:**<br/> Die Position (Index, Integer) des Kapitels innerhalb des Inhalts.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Classification </li> <li> **Berichtsname:**<br/> Kapitelposition </li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>position) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.index </li> <li> **XDM-Feldpfad für Sammlung:**<br/> mediaCollection.chapterDetails.index </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### Kapiteloffset

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/> media.chapter.offset </li> <li> **Erforderlich:**<br/> SDK: Nein; API: Ja. </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> Chapter Close </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> 58 </li><li> **Beschreibung:**<br/> Offset des Kapitels innerhalb des Inhalts ab Beginn (in Sekunden).   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Classification </li> <li> **Berichtsname:**<br/> Kapiteloffset </li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.offset </li> <li> **XDM-Feldpfad für Sammlung:**<br/> mediaCollection.chapterDetails.offset </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### Kapitellänge

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/> media.chapter.length </li> <li> **Erforderlich:**<br/> SDK: Nein; API: Ja. </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> Chapter Close </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> 486 </li><li> **Beschreibung:**<br/> Die Länge des Kapitels in Sekunden.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **Heartbeat:**<br/> (l:stream:chapter_length) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Classification </li> <li> **Berichtsname:**<br/> Kapitellänge </li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>length) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>length) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.xmpDM:duration </li> <li> **XDM-Feldpfad für Sammlung:**<br/> mediaCollection.chapterDetails.length </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### Kapitel

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> nein </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Chapter Close </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/> Die automatisch generierte ID des Kapitels.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> eVar </li> <li> **Gültigkeit:**<br/> bei HIT </li> <li> **Berichtsname:**<br/> Kapitel </li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>name) </li> <li> **Daten-Feed:**<br/> videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.@id </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.ID </li> </ul> |

## Kapitelmetriken {#chapter-Metrics}

### Chapter Start

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt  </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Chapter Start </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/> Die Anzahl der Kapitelstarts.  **Wichtig:** Wenn dieses Ereignis festgelegt wurde, lautet der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Ereignis </li> <li> **Berichtsname:**<br/> Kapitelstarts</li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>view) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>view) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.chapterCount.<br/>value > 0 => „TRUE“ </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### Kapitelbeendigung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt  </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zeichenfolge </li> <li> **Gesendet mit:**<br/> Chapter Close </li> <li> **Min. SDK-Version:** 1.3</li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/> Die Anzahl der Kapitelbeendigungen.  **Wichtig:** Wenn dieses Ereignis festgelegt wurde, lautet der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Ereignis </li> <li> **Berichtsname:**<br/> Kapitelbeendigungen</li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.mediaChapter.<br/>completes.value </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### Besuchszeit für Kapitel

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-Schlüssel:**<br/> automatisch festgelegt  </li> <li> **API-Schlüssel:**<br/> nicht verfügbar </li> <li> **Erforderlich:**<br/> ja </li> <li> **Typ:**<br/> Zahl </li> <li> **Gesendet mit:**<br/> Chapter Close </li> <li> **Min. SDK-Version:** 1.3 </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/> Die mit dem Kapitel verbrachte Zeit.  Der Wert wird im Zeitformat (HH:MM:SS) in Analysis Workspace und in Reports &amp; Analytics angezeigt. In Daten-Feeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Verfügbar:**<br/> ja </li> <li> **Reservierte Variable:**<br/> Ereignis </li> <li> **Berichtname:**<br/> Besuchszeit für Kapitel</li> <li> **Kontextdaten:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Daten-Feed:**<br/> nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> <li> **XDM-Feldpfad:**<br/> media.mediaTimed.mediaChapter.<br/>timePlayed.value </li> <li> **XDM-Feldpfad für Berichterstellung:**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## Verwandte APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
