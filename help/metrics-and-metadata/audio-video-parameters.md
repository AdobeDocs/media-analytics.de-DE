---
seo-title: Audio- und Videoparameter
title: Audio- und Videoparameter
uuid: fdacfb 8 b-db 3 e -46 fb-b 9 ad-c 3 a 749555 b 2 a
translation-type: tm+mt
source-git-commit: 6ce1ded12ff64962edb614f436e40f05b65dff34

---


# Audio- und Videoparameter{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Am 7. Februar 2019 veröffentlichte Adobe Analytics für Video und Audio eine Änderung des Metriknamens. <i>Medienaufrufe</i> wird nun als <i>Medienstarts</i> bezeichnet. Diese Änderung wurde vorgenommen, um Branchenstandards in Metriken und Berichten widerzuspiegeln und die Metrik in Berichten leicht erkennbar zu machen.

>[!NOTE]
>
>Am 13. September 2018 wurde eine Änderung an den Beschriftungen für einige Dimensionen, Metriken und Berichte vorgenommen, um die inhaltsübergreifende Verfolgung von Video- und Audioanalysen zu ermöglichen. Zu den geänderten Bezeichnungen gehören: *Videoaufrufe* in *Medienaufrufe*, *Videolänge* in *Inhaltsdauer* und *Videoname* in *Inhaltsname*. Die Videoberichte in Reports and Analytics wurden alle aktualisiert und verwenden nun den Begriff „Medien“ statt „Video“. Die Bezeichnungsänderungen haben sich weder auf die Datenerfassung noch auf die historischen Daten ausgewirkt. Bitte beachten Sie diese Änderungen, falls Sie diese im Report Builder oder in anderen externen automatisierten Daten-Pulls verwenden, die von dieser Änderung betroffen sein könnten.

Dieses Thema enthält eine Liste von Audio- und Videoinhaltsdaten, einschließlich Kontextdatenwerten, die Adobe über Lösungsvariablen sammelt.

Beschreibung der Tabellendaten:

* **Implementierung:** Informationen zu Implementierungswerten und -anforderungen.
   * *Schlüssel:* Variable, die entweder manuell in der App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich*: Gibt an, ob der Parameter für das einfache Audio- und Video-Tracking erforderlich ist.
   * *Typ:* Gibt den Typ der Variablen (Zeichenfolge oder Zahl) an.
   * *Gesendet Mit* : Zeigt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf, der beim Medienstart gesendet wird, *Anzeigenstart* ist der Analytics-Aufruf, der beim Anzeigenstart gesendet wird usw. *Die Aufrufe schließen* sind die kompilierten Analyseaufrufe, die direkt vom Heartbeat-Server an den Analytics-Server am Ende der Mediensitzung oder am Ende der Anzeige, Kapitel usw. gesendet werden. Die Schließen-Aufrufe sind in Netzwerkpaketaufrufen nicht verfügbar.
   * *Min. SDK-Version:* Gibt die SDK-Version an, die Sie benötigen, um auf den Parameter zuzugreifen.
   * *Beispielwert:* Bietet ein Beispiel für häufige Variablenverwendung.
* **Netzwerkparameter:** Zeigt die Werte an, die an Adobe Analytics- oder Heartbeat-Server übergeben werden. Diese Spalte enthält die Namen der Parameter, die in von Adobe Media SDKs generierten Netzwerkaufrufen enthalten sind.
* **Reporting:** Informationen zur Anzeige und Analyse der Audio- und Videodaten.
   * *Verfügbar:* Gibt an, ob die Daten standardmäßig in Berichten verfügbar sind (*Ja*) oder manuell eingerichtet werden müssen (*Anwenderspezifisch*).
   * *Reservierte Variablen:* Gibt an, ob die Daten als Ereignis, eVar, Prop oder Classification in einer reservierten Variablen erfasst werden.
   * *Ablauf:* Gibt an, ob die Daten nach jedem Hit oder nach jedem Besuch ablaufen.
   * *Berichtsname:* Name des Adobe Analytics-Berichts für die Variable
   * *Kontextdaten:* Name der Adobe Analytics-Kontextdaten, die an den Reporting-Server übergeben und in Verarbeitungsregeln verwendet werden.
   * *Datenfeed:* Spaltenname für die Variable in Clickstream- oder Live-Stream-Datenfeeds
   * *Audience Manager:* Eigenschaftsname in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändern Sie nicht die Classification-Namen für die unten aufgeführten Variablen, die unter Berichterstellung/Reservierte Variable als "Classification" beschrieben werden.\
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für die Medienverfolgung aktiviert ist. Von Zeit zu Zeit fügt Adobe neue Eigenschaften hinzu. Falls dies eintritt, müssen Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften zu erhalten. Während des Aktualisierungsprozesses bestimmt Adobe, ob die Klassifizierungen durch Überprüfen der Namen der Variablen aktiviert werden. Wenn eine davon fehlt, fügt Adobe die fehlenden Felder wieder hinzu.

## Core-Audio- und Videodaten {#section_y55_y1m_n1b}

### Streamtyp {#stream-type}

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.streamType </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK Version:** 2.2 <br/><br/>Available in [Media Collection API Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li>  <li> **Probenwert:** <br/>„Video“  </li> <li> **Beschreibung:**<br/> Gibt den Stream-Typ an. Gültige Werte sind „audio“, „video“ und „“.  <br/><br/>[Segmente](../metrics-and-metadata/segments.md): <br/><br/>Streamtype "All" - Segmentieren Sie alle Medienstreamdaten. <br/> **Regel:** Inhalt (ID) existiert <br/><br/>streamtype "Audio" - Alle Audiostreamdaten werden segmentiert. <br/>**Regel:** Inhalt (ID) vorhanden UND Stream-Typ = Audio <br/><br/>streamtype "Video" - Alle Videostreamdaten werden segmentiert. <br/>**Regel:** Inhalt (ID) vorhanden UND Streamtyp = Video <br/><br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. streamtype) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. streamtype) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Inhalt </li> <li> **Kontextdaten:**<br/> (a. media. streamtype) </li> <li> **Datenfeed:** <br/>videostreamtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Inhalts-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.id </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"4586695ABC"  </li> <li>**Beschreibung:**<br/> Inhalts-ID des Inhalts, der verwendet werden kann, um zurück zu anderen Branchen/CMS-IDs zurückzukommen, gleich dem letzten Wert von `s:asset:video_id` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Heartbeats:**<br/> (s: Asset: video_ id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Inhalt </li> <li> **Kontextdaten:**<br/> (a. media. name) </li> <li> **Datenfeed:**<br/>video </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Inhaltsdauer (Variable)

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.length </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> VOD: 128; Live: 86400; Linear: 1800. </li><li> **Beschreibung:**<br/> Länge der Clips/Laufzeit: Dies ist die maximale Länge (oder Dauer) des Inhalts (in Sekunden). It equals the last value of `l:asset:length` from events of type Main. <br/>Wird `l:asset:length` nicht festgelegt, wird der letzte Wert verwendet `l:asset:duration` . <br/>Im Reporting stellt „Videolänge“ die Klassifikation und „Inhaltsdauer (Variable)“ die eVAR dar.  <br/> **Wichtig:** Diese Eigenschaft wird verwendet, um verschiedene Metriken zu berechnen, z. B. Metriken für Fortschritts-Tracking und Zielgruppendurchschnitt pro Minute. Wenn sie nicht festgelegt ist oder kleiner/gleich null ist, sind diese Metriken nicht verfügbar.  Bei Live-Medien mit unbekannter Dauer wird standardmäßig der Wert „86400“ verwendet. <br/>Pre Version 1.5.1, dies `l:asset:duration`war; nach 1.5.1, ist dies `l:asset:length.`<br/> **Releasedatum: 13.09.2018** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Heartbeats:**<br/> (l: Asset: length) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Inhaltsdauer (Variable) </li> <li> **Kontextdaten:**<br/> (a. media. length) </li> <li> **Datenfeed:**<br/>videolength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Videolänge

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.length </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> VOD: 128; Live: 86400; Linear: 1800. </li> <li> **Beschreibung:**<br/> Länge der Clips/Laufzeit: Dies ist die maximale Länge (oder Dauer) des Inhalts (in Sekunden). Sie entspricht dem letzten Wert von l:asset:length der Ereignisse des Typs „Main“. Wenn l:asset:length nicht festgelegt ist, wird der letzte Wert von l:asset:duration verwendet. Im Reporting stellt „Videolänge“ die Klassifikation und „Inhaltsdauer (Variable)“ die eVAR dar.  <br/> **Wichtig:** Diese Eigenschaft wird verwendet, um verschiedene Metriken zu berechnen, z. B. Metriken für Fortschritts-Tracking und Zielgruppendurchschnitt pro Minute. Wenn sie nicht festgelegt ist oder kleiner/gleich null ist, sind diese Metriken nicht verfügbar.  Bei Live-Medien mit unbekannter Dauer wird standardmäßig der Wert „86400“ verwendet. Pre Version 1.5.1, this was l:asset:duration; after 1.5.1, this is l:asset:length.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Heartbeats:**<br/> (l: Asset: length) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Videodauer </li> <li> **Kontextdaten:**<br/> (a. media. length) </li> <li> **Datenfeed:** <br/>videoclassificationlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Content-Typ

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.contentType </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>beschränkte Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"vod" </li> <li> **Beschreibung:**<br/> Verfügbare Werte pro **Stream-Typ**: <br/> _Audio:_ " song "," podcast "," audiobook "," radio " <br/> _Video:_ " Vod "," Live "," Linear "," UGC "," dvod " <br/> Kunden können benutzerdefinierte Werte für diesen Parameter bereitstellen. This equals `s:stream:type.` If that is unset, this equals missing_content_type. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. contenttype) </li> <li> **Heartbeats:**<br/> (s: stream: type) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Content-Typ </li> <li> **Kontextdaten:**<br/> (a. contenttype) </li> <li> **Datenfeed:**<br/>videocontenttype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.<br/>contenttype) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Mediensitzungs-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>vom Backend abgerufen </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.8 </li> <li> **Beispielwert:**<br/> 1482236761294786918253 </li> <li> **Beschreibung:**<br/> Hiermit wird eine Instanz eines eindeutigen Inhalts identifiziert, der für eine einzelne Wiedergabe eindeutig ist.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. vsid) </li> <li> **Heartbeat:**<br/> (s: Ereignis: sid) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a. media. vsid) </li> <li> **Datenfeed:**<br/>vsid </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vsid) </li> </ul> |

### Inhalts-Player-Name

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.playerName </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> " Brightcove " </li> <li> **Beschreibung:**<br/> Name des Players.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>playerName) </li> <li> **Heartbeats:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Inhalts-Player-Name </li> <li> **Kontextdaten:**<br/> (a. media. playername) </li> <li> **Datenfeed:**<br/>videoplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.playerName) </li> </ul> |

### Inhaltskanal

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [Kanal](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.channel </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"Sports" </li> <li> **Beschreibung:**<br/> Distribution-Rechner/Kanäle oder der Inhalt des Inhalts. Hier sind beliebige Zeichenfolgen zulässig.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. channel) </li> <li> **Heartbeats:**<br/> (s: sp: channel) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtstyp:**<br/>Inhaltskanal </li> <li> **Kontextdaten:**<br/> (a. media. channel) </li> <li> **Datenfeed:**<br/>videochannel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.channel) </li> </ul> |

### Inhaltssegment

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> " 0-10 " </li> <li> **Beschreibung:**<br/> Das Intervall, das den Teil des Inhalts beschreibt, der angezeigt wurde (in Minuten). Das Segment wird als Mindest- und Höchstwert der Werte der Abspielleiste bei einer Wiedergabesitzung berechnet.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Inhaltssegment </li> <li> **Kontextdaten:**<br/> (a. media. segment) </li> <li> **Datenfeed:**<br/>videosegment </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segment) </li> </ul> |

### Inhaltsname (Variable)

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.name </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/>"The Big Bang Theory" </li> <li> **Beschreibung:**<br/> In Berichten ist der Videoname die Classification und der Inhaltsname (Variable) die evar. Der Anzeigename (von Menschen lesbar) des Inhalts. Entspricht dem letzten Wert von `s:asset:name.` <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Heartbeats:**<br/> (s: Asset: name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Inhaltsname (Variable) </li> <li> **Kontextdaten:**<br/> (a. media. friendlyname) </li> <li> **Datenfeed:**<br/>videoname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Videoname

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.name </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/>"The Big Bang Theory" </li> <li> **Beschreibung:**<br/> Dies ist der benutzerfreundliche (lesbare) Name des Inhalts, gleich dem letzten Wert in `s:asset:name.`<br/>der Berichterstellung, der Videoname ist die Classification und der Inhaltsname (Variable) ist die evar. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Heartbeats:**<br/> (s: Asset: name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Videoname </li> <li> **Kontextdaten:**<br/> (a. media. friendlyname) </li> <li> **Datenfeed:** <br/>videoclassificationname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Videopfad

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"4586695ABC"  </li> <li> **Beschreibung:**<br/> Möglichkeit zur Verfolgung des Pfades des Viewers über die Site und/oder App, um den Pfad zu erkennen, den sie zum Anzeigen eines bestimmten Videos eingeschlagen haben. Beliebige Integer- und/oder Buchstaben-Kombination.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Heartbeats:**<br/> (s: Asset: video_ id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Prop </li> <li> **Berichtsname:**<br/>Videopfad </li> <li> **Kontextdaten:**<br/> (a. media. name) </li> <li> **Datenfeed:**<br/>videopath </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

### SDK-Version

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.sdkVersion </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>"2.62.0_release" </li> <li> **Beschreibung:**<br/> Die SDK-Version, die vom Player verwendet wird. Hier ist jeder Wert möglich, der für Ihren Player sinnvoll ist. <br/><br/>Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Sdkversion) </li> <li> **Heartbeats:**<br/> (s: sp: sdk) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. sdkversion) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL-Version

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **Beschreibung:**<br/> Die Heartbeat SDK-Version, die für die Tracking-Sitzung verwendet wird. <br/><br/>Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  <br/><br/>[Mediaheartbeat. version ();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Vhlversion) </li> <li> **Heartbeats:**<br/> (s: sp: hb_ version) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a. media. vhlversion) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Standard-Audio- und Videometadaten {#section_pfc_hbm_n1b}

### Show

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SHOW </li> <li> **API-Schlüssel:**<br/>media.show </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " Modern Family "" Blacklist "" New Girl " </li> <li> **Beschreibung:**<br/> Programmname für Programm-/Reihenname <br/>ist nur erforderlich, wenn die Anzeige Teil einer Reihe ist.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. show) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. show) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Serie </li> <li> **Kontextdaten:**<br/> (a. media. show) </li> <li> **Datenfeed:**<br/>videoshow </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.show) </li> </ul> |

### Stream-Format

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>STREAM_FORMAT </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>"Live" </li> <li> **Beschreibung:**<br/> Format des Streams (Live, VOD, Linear).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. format) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. format) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a. media. format) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.format) </li> </ul> |

### Staffel

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SEASON </li> <li> **API-Schlüssel:**<br/>media.season </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " 2 " </li> <li> **Beschreibung:**<br/> Die Jahresnummer, zu der die Anzeige gehört. Die Saisonserie ist nur erforderlich, wenn die Anzeige Teil einer Reihe ist.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. season) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. season) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Staffel </li> <li> **Kontextdaten:**<br/> (a. media. season) </li> <li> **Datenfeed:**<br/>videoseason </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.season) </li> </ul> |

### Episode

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>EPISODE </li> <li> **API-Schlüssel:**<br/>media.episode </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " 13 " </li> <li> **Beschreibung:**<br/> Die Anzahl der Folge.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. episode) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. episode) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Episode </li> <li> **Kontextdaten:**<br/> (a. media. episode) </li> <li> **Datenfeed:**<br/>videoepisode </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.episode) </li> </ul> |

### Element-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ASSET_ID </li> <li> **API-Schlüssel:**<br/>media.assetId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " 89745363 " </li> <li> **Beschreibung:**<br/> Dies ist die eindeutige Kennung für den Inhalt des Medienassets, z. B. Episodenbezeichner für TV-Serie, Film-Asset-ID oder Live-Ereigniskennung. In der Regel werden diese IDs von Metadaten-Anbietern wie EIDR, TMS/Gracenote oder Rovi abgerufen. Diese IDs können auch von anderen speziellen oder internen Systemen stammen.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. asset) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. asset) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/> Asset-ID </li> <li> **Kontextdaten:**<br/> (a. media. asset) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.asset) </li> </ul> |

### Genre

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>GENRE </li> <li> **API-Schlüssel:**<br/>media.genre </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " Drama "," Comedy " </li> <li> **Beschreibung:**<br/> Geben oder gruppieren Sie Inhalte gemäß den vom Content Producer definierten Inhalten. Die Werte müssen bei der Variablenimplementierung durch Kommas getrennt werden. In Berichten teilt die Listen-eVar jeden Wert in zwei Zeileneinträge auf, von denen jeder die gleiche Metrikgewichtung erhält.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. genre) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. genre) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Listen-eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Genre </li> <li> **Kontextdaten:**<br/> (a. media. genre) </li> <li> **Datenfeed:**<br/>videogenre </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.genre) </li> </ul> |

### Erstes Sendedatum

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FIRST_AIR_DATE </li> <li> **API-Schlüssel:**<br/>media.firstAirDate </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " 2016-01-25 « </li> <li> **Beschreibung:**<br/> Das Datum, an dem der Inhalt beim ersten Mal im Fernsehen gezeichnet wurde. Hier kann jedes Datumsformat verwendet werden, jedoch empfiehlt Adobe JJJJ-MM-TT. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. airdate) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. airdate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Erstes Sendedatum </li> <li> **Kontextdaten:**<br/> (a. media. airdate) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.airDate) </li> </ul> |

### Erstes digitales Veröffentlichungsdatum

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FIRST_DIGITAL_DATE </li> <li> **API-Schlüssel:**<br/>media.firstDigitalDate </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " 2016-01-25 « </li> <li> **Beschreibung:**<br/> Das Datum, an dem der Inhalt auf einem digitalen Kanal oder in einer anderen Plattform angezeigt wird. Hier kann jedes Datumsformat verwendet werden, jedoch empfiehlt Adobe JJJJ-MM-TT. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. digitaldate) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. digitaldate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/> Erstes digitales Veröffentlichungsdatum </li> <li> **Kontextdaten:**<br/> (a. media. digitaldate) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Inhaltsbewertung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>RATING </li> <li> **API-Schlüssel:**<br/>media.rating </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> TVY, TVG, TVPG, TVMA </li> <li> **Beschreibung:**<br/> Bewertung gemäß der TV-Elterlichen Richtlinien.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. rating) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. rating) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Inhaltsbewertung </li> <li> **Kontextdaten:**<br/> (a. media. rating) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.rating) </li> </ul> |

### Urheber

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ORIGINATOR </li> <li> **API-Schlüssel:**<br/>media.originator </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " Warner Brothers "," Sony "," Disney " </li> <li> **Beschreibung:**<br/> Ersteller des Inhalts.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. originator) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. originator) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/> Urheber </li> <li> **Kontextdaten:**<br/> (a. media. originator) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.originator) </li> </ul> |

### Netzwerk

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>NETWORK </li> <li> **API-Schlüssel:**<br/>media.network </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " Fox "," Bravo "," ESPN " </li> <li> **Beschreibung:**<br/> Der Netzwerk-/Kanalname.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. network) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. network) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Netzwerk </li> <li> **Kontextdaten:**<br/> (a. media. network) </li> <li> **Datenfeed:**<br/>videonetwork </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.network) </li> </ul> |

### Sendungstyp

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SHOW_TYPE </li> <li> **API-Schlüssel:**<br/>media.showType </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " 0 " = Volle Folge; " 1 " = Preview/Trailer; " 2 " = Clip; " 3 " = Sonstige. </li> <li> **Beschreibung:**<br/> Inhaltstyp, ausgedrückt als Ganzzahl zwischen 0 und 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. type) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. type) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Serientyp </li> <li> **Kontextdaten:**<br/> (a. media. type) </li> <li> **Datenfeed:**<br/>videoshowtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>MVPD </li> <li> **API-Schlüssel:**<br/>media.pass.mvpd </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " Comcast "," directv "," Dish " </li> <li> **Beschreibung:**<br/> MVPD, die über die Adobe-Authentifizierung bereitgestellt wird.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. mvpd) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. pass.<br/>mvpd) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>MVPD </li> <li> **Kontextdaten:**<br/> (a. media. pass. mvpd) </li> <li> **Datenfeed:**<br/>videomvpd </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorisiert

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>AUTHORIZED </li> <li> **API-Schlüssel:**<br/>media.pass.auth </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " TRUE " </li> <li> **Beschreibung:**<br/> Der Benutzer wurde über adobepass autorisiert. <br/>**Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. auth) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. pass.<br/>Auth) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Autorisiert </li> <li> **Kontextdaten:**<br/> (a. media. pass. auth) </li> <li> **Datenfeed:**<br/>videoauthorized </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Tagesteil

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>DAY_PART </li> <li> **API-Schlüssel:**<br/>media.dayPart </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li> <li> **Beschreibung:**<br/> Eine Eigenschaft, die die Uhrzeit des Tages definiert, an dem der Inhalt übertragen oder wiedergegeben wurde. Hier können Kunden jeden erforderlichen Wert festlegen.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. daypart) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. daypart) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Tagesteil </li> <li> **Kontextdaten:**<br/> (a. media. daypart) </li> <li> **Datenfeed:**<br/>videodaypart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.dayPart) </li> </ul> |

### Medien-Feed-Typ

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FEED </li> <li> **API-Schlüssel:**<br/>media.feed </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> " East-HD "," West-HD "," East-SD " </li> <li> **Beschreibung:**<br/> Feed-Typ. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. feed) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. feed) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Medien-Feed-Typ </li> <li> **Kontextdaten:**<br/> (a. media. feed) </li> <li> **Datenfeed:**<br/>videofeedtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.feed) </li> </ul> |

### Künstler

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.artist </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„Die Beatles“ </li> <li> **Beschreibung:**<br/> Name des Künstlers. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. artist) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. artist) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. artist) </li> <li> **Datenfeed:** <br/>videoaudioartist </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.artist) </li> </ul> |

### Album

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.album </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/>„Revolver“ </li> <li> **Beschreibung:**<br/> Name des Albums. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. album) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. album) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. album) </li> <li> **Datenfeed:** <br/>videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.album) </li> </ul> |

### Beschriftung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.label </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/>„Revolver“ </li> <li> **Beschreibung:**<br/> Name der Datensatzbeschriftung. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. label) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. label) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. label) </li> <li> **Datenfeed:** <br/>videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.author </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„John Kennedy Toole“ </li> <li> **Beschreibung:**<br/> Name des Autors (eines Audiobuchs). <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. author) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. author) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. author) </li> <li> **Datenfeed:** <br/>videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.author) </li> </ul> |

### Station

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.station </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„NPR“ </li> <li> **Beschreibung:**<br/> Name/ID des Radioders. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. station) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. station) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. station) </li> <li> **Datenfeed:**<br/>videoaudiostation </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.station) </li> </ul> |

### Publisher

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.publisher </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„Random Bauhaus“ </li> <li> **Beschreibung:**<br/> Name des Herausgebers des Audioinhalts. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. publisher) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. publisher) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. publisher) </li> <li> **Datenfeed:**<br/>videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.publisher) </li> </ul> |

## Audio- und Videometriken {#section_3D5F9C555274428AA6030D07596177E9}

### Medienstarts

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/> Medienstart</li> <li> **Min. SDK-Version:** beliebig</li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Ereignis für das Medium. (Tritt auf, wenn der Zuschauer auf die _Play_-Schaltfläche klickt). Gilt auch, wenn Pre-Roll-Anzeigen, Puffern, Fehler usw. auftreten.  <br/>**Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. view) </li> <li> **Heartbeats:**<br/> (s: Ereignis:<br/>type = start) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> Medienstarts </li> <li> **Kontextdaten:**<br/> (a. media. view) </li> <li> **Datenfeed:**<br/>videostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.view) </li> </ul> |

### Inhaltsstarts

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Das erste Bild von Medien wird verwendet. Wenn der Anwender den Inhalt während einer Anzeige, eines Puffervorgangs usw. verlässt, tritt kein Content Start-Ereignis auf.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Inhaltsstarts </li> <li> **Kontextdaten:**<br/> (a. media. play) </li> <li> **Datenfeed:**<br/>videoplay </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.play) </li> </ul> |

### Inhaltsbeendigung {#content-complete}

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Ein Stream, der bis zum Abschluss angesehen wurde. Dies bedeutet nicht unbedingt, dass der Benutzer den gesamten Stream überwacht oder überwacht hat; sie könnten weiter übersprungen worden sein. Dies bedeutet nur, dass der Benutzer das Ende des Streams erreicht hat, 100%. <br/>Siehe [auch Sitzungsende](quality-parameters.md#session-end)<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/> (s: Ereignis:<br/>type = complete) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Inhaltsbeendigungen </li> <li> **Kontextdaten:**<br/> (a. media. complete) </li> <li> **Datenfeed:**<br/>videocomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.complete) </li> </ul> |

### Inhaltsbesuchszeit

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 105 </li> <li> **Beschreibung:**<br/> Summiert die Ereignisdauer (in Sekunden) für alle Ereignisse des Typs PLAY im Hauptinhalt. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Besuchszeit für Inhalt </li> <li> **Kontextdaten:**<br/> (a. media. timeplayed) </li> <li> **Datenfeed:**<br/>videotime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Besuchszeit für Medien

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 120 </li> <li> **Beschreibung:**<br/> Summiert die Ereignisdauer (in Sekunden) für alle Ereignisse des Typs PLAY, sowohl Hauptinhalt als auch Anzeigeninhalt. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Besuchszeit für Medien </li> <li> **Kontextdaten:**<br/> (a. media. totaltimeplayed) </li> <li> **Datenfeed:**<br/>videototaltime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Eindeutige Spielzeit

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 94 </li> <li> **Beschreibung:**<br/> Der Wert in Sekunden der eindeutigen Inhaltssegmente, die während einer Sitzung wiedergegeben werden. Ausgenommen sind Szenarios mit Suchvorgängen, in denen ein Betrachter das gleiche Segment des Inhalts mehrmals betrachtet.  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a. media. uniquetimeplayed) </li> <li> **Datenfeed:**<br/>videouniquetimeplayed </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. uniquetimeplayed) </li> </ul> |

### 10 Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Abspielkopf übergibt die 10%-Marke des Inhalts basierend auf der Länge. Die Markierung wird nur einmal gezählt, selbst wenn der Benutzer zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>10 % Fortschrittsmarkierung </li> <li> **Kontextdaten:**<br/> (a. media. progress 10) </li> <li> **Datenfeed:**<br/>videoprogress10 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress10) </li> </ul> |

### Fünfundzwanzig % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Der Abspielkopf übergibt die 25%-Marke des Inhalts basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>25 % Fortschrittsmarkierung </li> <li> **Kontextdaten:**<br/> (a. media. progress 25) </li> <li> **Datenfeed:**<br/>videoprogress25 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress25) </li> </ul> |

### 5% Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Der Abspielkopf übergibt die 50%-Marke des Inhalts basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>50 % Fortschrittsmarkierung </li> <li> **Kontextdaten:**<br/> (a. media. progress 50) </li> <li> **Datenfeed:**<br/>videoprogress50 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress50) </li> </ul> |

### Seventy-Five % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> **Nicht zutreffend** </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Der Abspielkopf übergibt die 75%-Marke basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>75 % Fortschrittsmarkierung </li> <li> **Kontextdaten:**<br/> (a. media. progress 75) </li> <li> **Datenfeed:**<br/>videoprogress75 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress75) </li> </ul> |

### Neunundsechzig % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Der Abspielkopf übergibt die 95%-Marke basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>95 % Fortschrittsmarkierung </li> <li> **Kontextdaten:**<br/> (a. media. progress 95) </li> <li> **Datenfeed:**<br/>videoprogress95 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress95) </li> </ul> |

### Zielgruppendurchschnitt pro Minute

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>Größer als oder gleich 1 </li> <li> **Beschreibung:**<br/> Die Metrik "Zielgruppendurchschnitt pro Minute" wird als Gesamtbesuchszeit für die Inhalte berechnet, die für ein bestimmtes Medienelement geteilt durch die Länge aller Wiedergabesitzung geteilt wird: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Zielgruppendurchschnitt pro Minute </li> <li> **Kontextdaten:**<br/> (a. media. averageminuteaudience) </li> <li> **Datenfeed:**<br/>videoaverageminuteaudience </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Geschätzte Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 - Eine Wiedergabe von 19 Minuten; <br/>2 - Für eine Wiedergabe von 31 Minuten; <br/>3 - Für eine Wiedergabe von 78 Minuten. </li> <li> **Beschreibung:**<br/> Die geschätzte Anzahl von Video- oder Audio-Streams pro einzelnen Inhalt. Dieser Wert wird je 30 Minuten Wiedergabezeit (Inhalt und Anzeigen) erhöht. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht. <br/><br/>Ein Stream wird alle 30 Minuten basierend auf dem `ms_s` (oder totaltimeplayed = Video Total Time) gezählt, ähnlich wie: <br/> `estimatedStreams = ` <br/> `&nbsp;&nbsp;FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> **Kontextdaten:**<br/> (a. media. estimatedstreams) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. estimatedstreams) </li> </ul> |

### Betroffene Streams pausiert

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Dieser Wert ist entweder "true" oder" false" . Er ist „true“, wenn während der Wiedergabe eines einzelnen Mediums mindestens eine Pause auftritt.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/> (s: Ereignis:<br/>type = pause) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Betroffene Streams pausiert </li> <li> **Kontextdaten:**<br/> (a. media. pause) </li> <li> **Datenfeed:**<br/>videopause </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pause) </li> </ul> |

### Pausierung – Ereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/> 2 </li> <li> **Beschreibung:**<br/> Diese Metrik wird als Anzahl der Pausenperioden berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/> (s: Ereignis:<br/>type = pause) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Pausierung – Ereignisse </li> <li> **Kontextdaten:**<br/> (a. media. pausecount) </li> <li> **Datenfeed:**<br/>videopausecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Pausierung – Gesamtdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/> 190 </li> <li> **Beschreibung:**<br/> Summiert die Dauer aller Ereignisse des Typs PAUSE (in Sekunden). Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Pausierung – Gesamtdauer </li> <li> **Kontextdaten:**<br/> (a. media. pausetime) </li> <li> **Datenfeed:**<br/>videopausetime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Inhaltswiederaufnahmen

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> **media.resume** </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Eine Wiederaufnahme wird für jede Wiedergabe gezählt, die nach über 30 Minuten Puffer, Pause oder Unterbrechung fortgesetzt wird ODER wenn dieser Wert vom Player in videoinfo trackplay festgelegt wird. <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/> (s: Ereignis:<br/>type = resume) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Inhaltswiederaufnahmen </li> <li> **Kontextdaten:**<br/> (a. media. resume) </li> <li> **Datenfeed:**<br/>videoresume </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.resume) </li> </ul> |

### Ansichten des Inhaltssegments

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> **Beschreibung:**<br/> Die Anzahl der Ansichten des Hauptinhalts. Eine Inhaltssegmentansicht wird gezählt, wenn mindestens ein Bild angezeigt wurde.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Ansichten des Inhaltssegments </li> <li> **Kontextdaten:**<br/> (a. media. segmentview) </li> <li> **Datenfeed:**<br/>videosegmentviews </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segmentView) </li> </ul> |

## Related APIs {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS: [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

