---
title: Audio- und Videoparameter
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Audio- und Videoparameter{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Am 7. Februar 2019 veröffentlichte Adobe Analytics für Video und Audio eine Änderung des Metriknamens. <i>Medienaufrufe</i> wird nun als <i>Medienstarts</i> bezeichnet. Diese Änderung wurde vorgenommen, um die Branchenstandards in Metriken und Berichten widerzuspiegeln und die Metrik in Berichten leicht identifizierbar zu machen.

>[!NOTE]
>
>Ab dem 13. September 2018 wurden die Beschriftungen für einige Dimensionen, Metriken und Berichte geändert, um eine inhaltsübergreifende Verfolgung der Video- und Audioanalyse zu ermöglichen. Zu den geänderten Bezeichnungen gehören: *Videoaufrufe* in *Medienaufrufe*, *Videolänge* in *Inhaltsdauer* und *Videoname* in *Inhaltsname*. Die Videoberichte in Reports and Analytics wurden alle aktualisiert und verwenden nun den Begriff „Medien“ statt „Video“. Die Bezeichnungsänderungen haben sich weder auf die Datenerfassung noch auf die historischen Daten ausgewirkt. Bitte beachten Sie diese Änderungen, falls Sie diese im Report Builder oder in anderen externen automatisierten Daten-Pulls verwenden, die von dieser Änderung betroffen sein könnten.

Dieses Thema enthält eine Liste von Audio- und Videoinhaltsdaten, einschließlich Kontextdatenwerten, die Adobe über Lösungsvariablen sammelt.

Beschreibung der Tabellendaten:

* **Implementierung:** Informationen zu Implementierungswerten und -anforderungen.
   * *Schlüssel:* Variable, die entweder manuell in der App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich*: Gibt an, ob der Parameter für das einfache Audio- und Video-Tracking erforderlich ist.
   * *Typ:* Gibt den Typ der Variablen (Zeichenfolge oder Zahl) an.
   * *Gesendet mit* - Gibt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf, der beim Medienstart gesendet wird, *Ad Start* ist der Analytics-Aufruf, der beim Anzeigenstart gesendet wird usw.; Die *Close* -Aufrufe sind die kompilierten Analytics-Aufrufe, die direkt vom Heartbeat-Server an den Analytics-Server am Ende der Mediensitzung oder am Ende der Anzeige, des Kapitels usw. gesendet werden. Die close-Aufrufe sind nicht in Netzwerkpaketaufrufen verfügbar.
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
>Ändern Sie nicht die Klassifizierungsnamen für die unten aufgeführten Variablen, die unter Berichterstellung/Reservierte Variable als "Klassifizierung"beschrieben werden.\
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für die Medienverfolgung aktiviert ist. Adobe fügt von Zeit zu Zeit neue Eigenschaften hinzu. In diesem Fall müssen Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften zu erhalten. Während des Aktualisierungsvorgangs ermittelt Adobe, ob die Klassifizierungen aktiviert sind, indem die Namen der Variablen überprüft werden. Wenn eines der Elemente fehlt, fügt Adobe die fehlenden erneut hinzu.

## Core-Audio- und Videodaten {#core-audio-and-video-data}

### Streamtyp {#stream-type}

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.streamType </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: 2.2 <br/><br/>Verfügbar in der Übersicht[ über die ](/help/media-collection-api/mc-api-overview.md)Media Collection-API oder [Download-SDKs - Versionen 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Probenwert:** <br/>„Video“  </li> <li> ****<br/> Beschreibung: Gibt den Stream-Typ an. Gültige Werte sind „audio“, „video“ und „“.  <br/><br/>[Berichtssegmente](/help/metrics-and-metadata/segments.md): <br/><br/>Medienstream-Typ: Alle - <br/>Segmentieren Sie alle Medienstream-Daten. Regel: Content (ID) exists <br/><br/>Media Stream Type: Audio - <br/>Segmentierung aller Audio-Stream-Daten; Regel: Content (ID) exists AND Media Stream Type = audio <br/><br/>Media Stream Type: "Video"- <br/>Segmentierung aller Videostream-Daten; Regel: Content (ID) existiert UND Media Stream Type != audio <br/><br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.streamType) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Inhalt </li> <li> ****<br/> Kontextdaten: (a.media.streamType) </li> <li> **Datenfeed:** <br/>videostreamtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Inhalts-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.id </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"4586695ABC"  </li> <li>****<br/> Beschreibung: Inhalts-ID des Inhalts, die verwendet werden kann, um eine Verbindung zu anderen Industrie-/CMS-IDs herzustellen, die dem letzten Wert von `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> ****<br/> Heartbeats: (s:asset:video_id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Inhalt </li> <li> ****<br/> Kontextdaten: (a.media.name) </li> <li> **Datenfeed:**<br/>video </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Inhaltsdauer (Variable)

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.length </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: VOD: 128; Live: 86400;Linear: 1800. </li><li> ****<br/> Beschreibung: Clip-Länge/Laufzeit - Dies ist die maximale Länge (oder Dauer) des verwendeten Inhalts (in Sekunden). It equals the last value of `l:asset:length` from events of type Main. <br/>Wenn `l:asset:length` kein Wert festgelegt ist, wird der letzte Wert von verwendet `l:asset:duration` . <br/>Im Reporting stellt „Videolänge“ die Klassifikation und „Inhaltsdauer (Variable)“ die eVAR dar.  <br/> **Wichtig:** Diese Eigenschaft wird verwendet, um verschiedene Metriken zu berechnen, z. B. Metriken für Fortschritts-Tracking und Zielgruppendurchschnitt pro Minute. Wenn sie nicht festgelegt ist oder kleiner/gleich null ist, sind diese Metriken nicht verfügbar.  Bei Live-Medien mit unbekannter Dauer wird standardmäßig der Wert „86400“ verwendet. <br/>Vor Version 1.5.1 war dies `l:asset:duration`der Fall; Nach 1.5.1 ist dies `l:asset:length.`<br/> **Releasedatum: 13.09.2018** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> ****<br/> Heartbeats: (l:asset:length) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Inhaltsdauer (Variable) </li> <li> ****<br/> Kontextdaten: (a.media.length) </li> <li> **Datenfeed:**<br/>videolength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Videolänge

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.length </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: VOD: 128; Live: 86400;Linear: 1800. </li> <li> ****<br/> Beschreibung: Clip-Länge/Laufzeit - Dies ist die maximale Länge (oder Dauer) des verwendeten Inhalts (in Sekunden). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. Im Reporting stellt „Videolänge“ die Klassifikation und „Inhaltsdauer (Variable)“ die eVAR dar.  <br/> **Wichtig:** Diese Eigenschaft wird verwendet, um verschiedene Metriken zu berechnen, z. B. Metriken für Fortschritts-Tracking und Zielgruppendurchschnitt pro Minute. Wenn sie nicht festgelegt ist oder kleiner/gleich null ist, sind diese Metriken nicht verfügbar.  Bei Live-Medien mit unbekannter Dauer wird standardmäßig der Wert „86400“ verwendet. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> ****<br/> Heartbeats: (l:asset:length) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Videodauer </li> <li> ****<br/> Kontextdaten: (a.media.length) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Content-Typ

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.contentType </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>beschränkte Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"vod" </li> <li> ****<br/> Beschreibung: Verfügbare Werte pro **Stream-Typ**: <br/> __ Audio: "song", "podcast", "audiobook", "radio" <br/> __ Video: "VoD", "Live", "Linear", "UGC", "DVoD" <br/> Kunden können benutzerdefinierte Werte für diesen Parameter bereitstellen. Dies entspricht `s:stream:type.` Wenn dies nicht festgelegt ist, ist dies gleich `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.contentType) </li> <li> ****<br/> Heartbeats: (s:stream:type) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Content-Typ </li> <li> ****<br/> Kontextdaten: (a.contentType) </li> <li> **Datenfeed:**<br/>videocontenttype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Mediensession-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>vom Backend abgerufen </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.8 </li> <li> ****<br/> Beispielwert: 1482236761294786918253 </li> <li> ****<br/> Beschreibung: Dadurch wird eine Instanz eines Inhaltsstreams identifiziert, die für eine einzelne Wiedergabe eindeutig ist.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.vsid) </li> <li> ****<br/> Heartbeat: (s:event:sid) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> ****<br/> Kontextdaten: (a.media.vsid) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Flag "Medien heruntergeladen"

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> `config.downloadedcontent` </li> <li> **API-Schlüssel:**<br/>vom Backend abgerufen </li> <li> **Erforderlich:**<br/>nein </li> <li> ****<br/> Typ: boolean </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: <br/>Starten Sie Android und iOS Extension v1.1.0 </li> <li> ****<br/> Beispielwert: true </li> <li> ****<br/> Beschreibung: Auf "true"setzen, wenn der Treffer aufgrund der Wiedergabe einer heruntergeladenen Inhaltsmediensitzung generiert wird. Nicht vorhanden, wenn heruntergeladene Inhalte nicht wiedergegeben werden.<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.download) </li> <li> ****<br/> Heartbeat: (s:meta:a.media.download) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> ****<br/> Kontextdaten: (a.media.download) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.download) </li> </ul> |

### Inhalts-Player-Name

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.playerName </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: "Brightcove" </li> <li> ****<br/> Beschreibung: Name des Players.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>playerName) </li> <li> ****<br/> Heartbeats: (s:sp:player_name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Inhalts-Player-Name </li> <li> ****<br/> Kontextdaten: (a.media.playerName) </li> <li> **Datenfeed:**<br/>videoplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Inhaltskanal

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [kanal](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.channel </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"Sports" </li> <li> ****<br/> Beschreibung: Verteilungs-Workstation/Kanäle oder Ort der Wiedergabe des Inhalts. Hier sind beliebige Zeichenfolgen zulässig.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.channel) </li> <li> ****<br/> Heartbeats: (s:sp:channel) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtstyp:**<br/>Inhaltskanal </li> <li> ****<br/> Kontextdaten: (a.media.channel) </li> <li> **Datenfeed:**<br/>videochannel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Inhaltssegment

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>ja </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: "0-10" </li> <li> ****<br/> Beschreibung: Das Intervall, das den Teil des Inhalts beschreibt, der angezeigt wurde (in Minuten). Das Segment wird als Mindest- und Höchstwert der Werte der Abspielleiste bei einer Wiedergabesitzung berechnet.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Inhaltssegment </li> <li> ****<br/> Kontextdaten: (a.media.segment) </li> <li> **Datenfeed:**<br/>videosegment </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Inhaltsname (Variable)

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.name </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/>"The Big Bang Theory" </li> <li> **Beschreibung:**<br/>Dies ist der "benutzerfreundliche"(für Menschen lesbare) Name des Inhalts, der dem letzten Wert von " `s:asset:name.`<br/>In"-Bericht entspricht. Videoname ist die Classification und Inhaltsname (Variable) ist die eVAR. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeats: (s:asset:name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Inhaltsname (Variable) </li> <li> ****<br/> Kontextdaten: (a.media.friendlyName) </li> <li> **Datenfeed:**<br/>videoname </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Videoname

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.name </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/>"The Big Bang Theory" </li> <li> ****<br/> Beschreibung: Dies ist der "benutzerfreundliche"(für Menschen lesbare) Name des Inhalts, der dem letzten Wert von " `s:asset:name.` <br/>In Reporting", "Videoname"die Klassifizierung und "Inhaltsname"(Variable) die eVAR entspricht.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeats: (s:asset:name) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Videoname </li> <li> ****<br/> Kontextdaten: (a.media.friendlyName) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Videopfad

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienstart </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>"4586695ABC"  </li> <li> ****<br/> Beschreibung: Bietet die Möglichkeit, den Pfad eines Viewers über eine Site und/oder App zu verfolgen, um den Pfad zu sehen, den sie zum Anzeigen eines bestimmten Videos verwendeten. Beliebige Integer- und/oder Buchstaben-Kombination.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> ****<br/> Heartbeats: (s:asset:video_id) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Prop </li> <li> **Berichtsname:**<br/>Videopfad </li> <li> ****<br/> Kontextdaten: (a.media.name) </li> <li> **Datenfeed:**<br/>videopath </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK-Version

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.sdkVersion </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>"2.62.0_release" </li> <li> ****<br/> Beschreibung: Die vom Player verwendete SDK-Version. Hier ist jeder Wert möglich, der für Ihren Player sinnvoll ist. <br/><br/>Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>sdkVersion) </li> <li> ****<br/> Heartbeats: (s:sp:sdk) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/> </li> <li> ****<br/> Kontextdaten: (a.media.sdkVersion) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL-Version

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> Beschreibung: Die für die Verfolgungssitzung verwendete Media SDK-Version. <br/><br/>Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>vhlVersion) </li> <li> ****<br/> Heartbeats: (s:sp:hb_version) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> ****<br/> Kontextdaten: (a.media.vhlVersion) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Standard-Audio- und Videometadaten {#standard-audio-and-video-metadata}

### Show

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SHOW </li> <li> **API-Schlüssel:**<br/>media.show </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "Modern Family" "Blacklist" "New Girl" </li> <li> ****<br/> Beschreibung: Programm-/Serienname <br/>Programmname ist nur erforderlich, wenn die Sendung Teil einer Reihe ist.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.show) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Serie </li> <li> ****<br/> Kontextdaten: (a.media.show) </li> <li> **Datenfeed:**<br/>videoshow </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.show) </li> </ul> |

### Stream-Format

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>STREAM_FORMAT </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>"Live" </li> <li> ****<br/> Beschreibung: Format des Streams (Live, VOD, Linear).  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.format) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> ****<br/> Kontextdaten: (a.media.format) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.format) </li> </ul> |

### Staffel

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SEASON </li> <li> **API-Schlüssel:**<br/>media.season </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "2" </li> <li> ****<br/> Beschreibung: Die Saisonnummer, zu der die Show gehört.  Die Saisonserie ist nur erforderlich, wenn die Sendung Teil einer Serie ist.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.season) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Staffel </li> <li> ****<br/> Kontextdaten: (a.media.season) </li> <li> **Datenfeed:**<br/>videoseason </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.season) </li> </ul> |

### Episode

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>EPISODE </li> <li> **API-Schlüssel:**<br/>media.episode </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: ‚13‘ </li> <li> ****<br/> Beschreibung: Die Anzahl der Folge.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.episode) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Episode </li> <li> ****<br/> Kontextdaten: (a.media.episode) </li> <li> **Datenfeed:**<br/>videoepisode </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.episode) </li> </ul> |

### Element-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ASSET_ID </li> <li> **API-Schlüssel:**<br/>media.assetId </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "89745363" </li> <li> ****<br/> Beschreibung: Dies ist die eindeutige ID für den Inhalt des Medienassets, z. B. die TV-Serienepisode-ID, die Filmeilenelement-ID oder die Live-Ereigniskennung. In der Regel werden diese IDs von Metadaten-Anbietern wie EIDR, TMS/Gracenote oder Rovi abgerufen. Diese IDs können auch von anderen speziellen oder internen Systemen stammen.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.asset) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/> Asset-ID </li> <li> ****<br/> Kontextdaten: (a.media.asset) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Genre

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>GENRE </li> <li> **API-Schlüssel:**<br/>media.genre </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "Drama", "Comedy" </li> <li> ****<br/> Beschreibung: Content-Typ oder -Gruppierung gemäß Definition des Content Producers. Die Werte müssen bei der Variablenimplementierung durch Kommas getrennt werden. In Berichten teilt die Listen-eVar jeden Wert in zwei Zeileneinträge auf, von denen jeder die gleiche Metrikgewichtung erhält.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.genre) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Listen-eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Genre </li> <li> ****<br/> Kontextdaten: (a.media.genre) </li> <li> **Datenfeed:**<br/>videogenre </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Erstes Sendedatum

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FIRST_AIR_DATE </li> <li> **API-Schlüssel:**<br/>media.firstAirDate </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienstart </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "2016-01-25" </li> <li> ****<br/> Beschreibung: Das Datum, an dem der Inhalt zum ersten Mal im Fernsehen gesendet wurde. Hier kann jedes Datumsformat verwendet werden, jedoch empfiehlt Adobe JJJJ-MM-TT. </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.airDate) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Erstes Sendedatum </li> <li> ****<br/> Kontextdaten: (a.media.airDate) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Erstes digitales Veröffentlichungsdatum

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FIRST_DIGITAL_DATE </li> <li> **API-Schlüssel:**<br/>media.firstDigitalDate </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "2016-01-25" </li> <li> ****<br/> Beschreibung: Das Datum, an dem der Inhalt zum ersten Mal auf einem beliebigen digitalen Kanal oder einer beliebigen Plattform gestrahlt wird. Hier kann jedes Datumsformat verwendet werden, jedoch empfiehlt Adobe JJJJ-MM-TT. </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.digitalDate) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/> Erstes digitales Veröffentlichungsdatum </li> <li> ****<br/> Kontextdaten: (a.media.digitalDate) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Inhaltsbewertung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>RATING </li> <li> **API-Schlüssel:**<br/>media.rating </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: TVY, TVG, TVPG, TVMA </li> <li> ****<br/> Beschreibung: Bewertung gemäß Definition in TV Elternrichtlinien.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.rating) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/>Inhaltsbewertung </li> <li> ****<br/> Kontextdaten: (a.media.rating) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Urheber

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ORIGINATOR </li> <li> **API-Schlüssel:**<br/>media.originator </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "Warner Brothers", "Sony", "Disney" </li> <li> ****<br/> Beschreibung: Ersteller des Inhalts.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.originator) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Classification </li> <li> **Berichtsname:**<br/> Urheber </li> <li> ****<br/> Kontextdaten: (a.media.originator) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Netzwerk

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>NETWORK </li> <li> **API-Schlüssel:**<br/>media.network </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "Fox", "Bravo", "ESPN" </li> <li> ****<br/> Beschreibung: Der Netzwerk-/Kanalname.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.network) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Netzwerk </li> <li> ****<br/> Kontextdaten: (a.media.network) </li> <li> **Datenfeed:**<br/>videonetwork </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.network) </li> </ul> |

### Sendungstyp

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SHOW_TYPE </li> <li> **API-Schlüssel:**<br/>media.showType </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "0" = vollständige Folge; "1" = Vorschau/Anhänger; "2" = Clip; "3" = Sonstige. </li> <li> ****<br/> Beschreibung: Inhaltstyp, ausgedrückt als Ganzzahl zwischen 0 und 3.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.type) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Serientyp </li> <li> ****<br/> Kontextdaten: (a.media.type) </li> <li> **Datenfeed:**<br/>videoshowtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>MVPD </li> <li> **API-Schlüssel:**<br/>media.pass.mvpd </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "Comcast", "DirecTV", "Dish" </li> <li> ****<br/> Beschreibung: MVPD wird über die Adobe-Authentifizierung bereitgestellt.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.mvpd) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>MVPD </li> <li> ****<br/> Kontextdaten: (a.media.pass.mvpd) </li> <li> **Datenfeed:**<br/>videomvpd </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorisiert

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>AUTHORIZED </li> <li> **API-Schlüssel:**<br/>media.pass.auth </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "TRUE" </li> <li> ****<br/> Beschreibung: Der Benutzer wurde über die Adobe-Authentifizierung autorisiert.  <br/>**Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.auth) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Autorisiert </li> <li> ****<br/> Kontextdaten: (a.media.pass.auth) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Tagesteil

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>DAY_PART </li> <li> **API-Schlüssel:**<br/>media.dayPart </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li> <li> ****<br/> Beschreibung: Eine Eigenschaft, die die Zeit des Tages definiert, an dem der Inhalt gesendet oder wiedergegeben wurde. Hier können Kunden jeden erforderlichen Wert festlegen.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.dayPart) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Tagesteil </li> <li> ****<br/> Kontextdaten: (a.media.dayPart) </li> <li> **Datenfeed:**<br/>videodaypart </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Medien-Feed-Typ

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FEED </li> <li> **API-Schlüssel:**<br/>media.feed </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> ****<br/> Beispielwert: "East-HD", "West-HD", "East-SD" </li> <li> ****<br/> Beschreibung: Feed-Typ.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.feed) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> Medien-Feed-Typ </li> <li> ****<br/> Kontextdaten: (a.media.feed) </li> <li> **Datenfeed:**<br/>videofeedtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Künstler

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.artist </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: 1.5.7 <br/>Verfügbar in Übersicht über die [Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder SDKs [herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„Die Beatles“ </li> <li> ****<br/> Beschreibung: Name des Künstlers.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.artist) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> ****<br/> Kontextdaten: (a.media.artist) </li> <li> **Datenfeed:** <br/>videoaudioartist </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.artist) </li> </ul> |

### Album

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.album </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: 1.5.7 <br/>Verfügbar in Übersicht über die [Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder SDKs [herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/>„Revolver“ </li> <li> ****<br/> Beschreibung: Name des Albums.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.album) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> ****<br/> Kontextdaten: (a.media.album) </li> <li> **Datenfeed:** <br/>videoaudioalbum </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.album) </li> </ul> |

### Beschriftung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.label </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: 1.5.7 <br/>Verfügbar in Übersicht über die [Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder SDKs [herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/>„Revolver“ </li> <li> ****<br/> Beschreibung: Name der Datensatzbeschriftung.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.label) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> ****<br/> Kontextdaten: (a.media.label) </li> <li> **Datenfeed:** <br/>videoaudiolabel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.author </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: 1.5.7 <br/>Verfügbar in Übersicht über die [Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder SDKs [herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„John Kennedy Toole“ </li> <li> ****<br/> Beschreibung: Name des Verfassers (eines Hörbuchs).  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.author) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> ****<br/> Kontextdaten: (a.media.author) </li> <li> **Datenfeed:** <br/>videoaudioauthor </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.author) </li> </ul> |

### Station

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.station </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: 1.5.7 <br/>Verfügbar in Übersicht über die [Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder SDKs [herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„NPR“ </li> <li> ****<br/> Beschreibung: Name/ID der Funkstation.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.station) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> ****<br/> Kontextdaten: (a.media.station) </li> <li> **Datenfeed:**<br/>videoaudiostation </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.station) </li> </ul> |

### Publisher

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.publisher </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Media Start, Media Close </li> <li> **Min.** SDK-Version: 1.5.7 <br/>Verfügbar in Übersicht über die [Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder SDKs [herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:** <br/>„Random Bauhaus“ </li> <li> ****<br/> Beschreibung: Name des Herausgebers des Audioinhalts.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.publisher) </li> <li> ****<br/> Heartbeats: (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/> </li> <li> ****<br/> Kontextdaten: (a.media.publisher) </li> <li> **Datenfeed:**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## Audio- und Videometriken {#audio-and-video-metrics}

### Medienstarts

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> ****<br/> Gesendet mit: Medienstart</li> <li> **Min. SDK-Version:** beliebig</li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Load-Ereignis für das Medium. (Tritt auf, wenn der Zuschauer auf die _Play_-Schaltfläche klickt). Gilt auch, wenn Pre-Roll-Anzeigen, Puffern, Fehler usw. auftreten.  <br/>**Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.view) </li> <li> ****<br/> Heartbeats: (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> ****<br/> Berichtsname: Medienstarts </li> <li> ****<br/> Kontextdaten: (a.media.view) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.view) </li> </ul> |

### Inhaltsstarts

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Das erste Medienbild wird genutzt. Wenn der Anwender den Inhalt während einer Anzeige, eines Puffervorgangs usw. verlässt, tritt kein Content Start-Ereignis auf.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Inhaltsstarts </li> <li> ****<br/> Kontextdaten: (a.media.play) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.play) </li> </ul> |

### Inhaltsbeendigung {#content-complete}

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Ein Stream, der bis zum Ende angesehen wurde. Dies bedeutet nicht unbedingt, dass der Benutzer den gesamten Stream angesehen oder angehört hat; Sie hätten voraus aussteigen können. Das bedeutet nur, dass der Benutzer das Ende des Streams zu 100 % erreicht hat. <br/>Siehe auch [Sitzungsende](quality-parameters.md#session-end)<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> ****<br/> Heartbeats: (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Inhaltsbeendigungen </li> <li> ****<br/> Kontextdaten: (a.media.complete) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Inhaltsbesuchszeit

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 105 </li> <li> ****<br/> Beschreibung: Speichert die Ereignisdauer (in Sekunden) für alle Ereignisse vom Typ PLAY im Hauptinhalt.  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Besuchszeit für Inhalt </li> <li> ****<br/> Kontextdaten: (a.media.timePlayed) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Besuchszeit für Medien

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 120 </li> <li> ****<br/> Beschreibung: Speichert die Ereignisdauer (in Sekunden) für alle Ereignisse vom Typ PLAY, sowohl Haupt- als auch Anzeigeninhalt.  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Besuchszeit für Medien </li> <li> ****<br/> Kontextdaten: (a.media.totalTimePlayed) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Eindeutige Spielzeit

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 94 </li> <li> ****<br/> Beschreibung: Der Wert in Sekunden der eindeutigen Segmente des Inhalts, die während einer Sitzung wiedergegeben wurden. Ausgenommen sind Szenarios mit Suchvorgängen, in denen ein Betrachter das gleiche Segment des Inhalts mehrmals betrachtet.  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> ****<br/> Kontextdaten: (a.media.uniqueTimePlayed) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### 10 % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Der Abspielkopf übergibt die 10 %-Marke des Inhalts basierend auf der Länge. Die Markierung wird nur einmal gezählt, selbst wenn der Benutzer zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>10 % Fortschrittsmarkierung </li> <li> ****<br/> Kontextdaten: (a.media.progress10) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25 % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Der Abspielkopf übergibt die 25 %-Marke des Inhalts basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>25 % Fortschrittsmarkierung </li> <li> ****<br/> Kontextdaten: (a.media.progress25) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### 50 % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Der Abspielkopf übergibt die 50 %-Marke des Inhalts basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>50 % Fortschrittsmarkierung </li> <li> ****<br/> Kontextdaten: (a.media.progress50) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### 75 % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> **Nicht zutreffend** </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Der Abspielkopf übergibt die 75 %-Marke des Inhalts basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>75 % Fortschrittsmarkierung </li> <li> ****<br/> Kontextdaten: (a.media.progress75) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95 % Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Der Abspielkopf übergibt die 95 %-Marke des Inhalts basierend auf der Inhaltslänge. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>95 % Fortschrittsmarkierung </li> <li> ****<br/> Kontextdaten: (a.media.progress95) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Zielgruppendurchschnitt pro Minute

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>Größer als oder gleich 1 </li> <li> ****<br/> Beschreibung: Die Metrik "Zielgruppe pro Minute"wird berechnet als "Besuchszeit insgesamt pro Inhalt"für ein bestimmtes Medienelement geteilt durch seine Länge für alle Wiedergabesitzungen: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Zielgruppendurchschnitt pro Minute </li> <li> ****<br/> Kontextdaten: (a.media.averageMinuteAudience) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Federated Data

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> ****<br/> Typ: boolean </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: true  </li> <li> ****<br/> Beschreibung: Auf "true"setzen, wenn der Treffer verknüpft ist (d. h. vom Kunden im Rahmen einer verknüpften Datenfreigabe empfangen wird, nicht bei der eigenen Implementierung). </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>nicht verfügbar </li> <li> ****<br/> Kontextdaten: (a.media.Federated) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.Federated) </li> </ul> |

### Geschätzte Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> ****<br/> Beispielwert: 1 - 19-minütige Wiedergabe; <br/>2 - Für eine Wiedergabe von 31 Minuten; <br/>3 - Für eine Wiedergabe von 78 Minuten. </li> <li> ****<br/> Beschreibung: Die geschätzte Anzahl der Video- oder Audio-Streams pro einzelnen Inhalt. Dieser Wert wird je 30 Minuten Wiedergabezeit (Inhalt und Anzeigen) erhöht. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht. <br/><br/>Ein Stream wird alle 30 Minuten basierend auf der `ms_s` (oder totalTimePlayed = Video Total Time) gezählt, ähnlich wie: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>anwenderspezifisch </li> <li> ****<br/> Kontextdaten: (a.media.effectiveStreams) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.effectiveStreams) </li> </ul> |

### Betroffene Streams pausiert

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Dieser Wert ist entweder true oder false. Er ist „true“, wenn während der Wiedergabe eines einzelnen Mediums mindestens eine Pause auftritt.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> ****<br/> Heartbeats: (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Betroffene Streams pausiert </li> <li> ****<br/> Kontextdaten: (a.media.pause) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Pausierung – Ereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> ****<br/> Beispielwert: 2 </li> <li> ****<br/> Beschreibung: Diese Metrik wird als Anzahl der Pausenzeiträume berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> ****<br/> Heartbeats: (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Pausierung – Ereignisse </li> <li> ****<br/> Kontextdaten: (a.media.pauseCount) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Pausierung – Gesamtdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zahl </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> ****<br/> Beispielwert: 190 </li> <li> ****<br/> Beschreibung: Gibt die Dauer (in Sekunden) aller Ereignisse des Typs PAUSE an. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Pausierung – Gesamtdauer </li> <li> ****<br/> Kontextdaten: (a.media.pauseTime) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Inhaltswiederaufnahmen

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> **media.resume** </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Eine Wiederaufnahme wird für jede Wiedergabe gezählt, die nach mehr als 30 Minuten Pufferzeit, Pause- oder Anhaltezeit fortgesetzt wird ODER wenn dieser Wert vom Player auf der VideoInfo trackPlay festgelegt wird. <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> ****<br/> Heartbeats: (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Inhaltswiederaufnahmen </li> <li> ****<br/> Kontextdaten: (a.media.resume) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Ansichten des Inhaltssegments

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> ****<br/> Gesendet mit: Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/>TRUE </li> <li> ****<br/> Beschreibung: Die Anzahl der Ansichten des Hauptinhalts. Eine Inhaltssegmentansicht wird gezählt, wenn mindestens ein Bild angezeigt wurde.  <br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/>nicht verfügbar </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Ansichten des Inhaltssegments </li> <li> ****<br/> Kontextdaten: (a.media.segmentView) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segmentView) </li> </ul> |

<!--
### Ad Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of ads started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.adCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Chapter Count 

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of chapters started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.chapterCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |
-->

## Parameter des California Consumer Privacy Act (CCPA) {#ccpa-params}

### Serverseitige Weiterleitung abwählen

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK-Schlüssel:Nicht zutreffend </li> <li> ****<br/> API-Schlüssel: analytics.optOutServerSideForwarding </li> <li> **Erforderlich:**<br/>nein </li> <li> ****<br/> Typ: boolean </li> <li> ****<br/> Gesendet mit: Medienstart </li> <li> **Min.** SDK-Version:Nicht zutreffend </li> <li> ****<br/> Beispielwert: true </li> <li>****<br/> Beschreibung: Auf "true"setzen, wenn der Endbenutzer die Freigabe seiner Daten für Adobe Analytics und andere Experience Cloud-Lösungen (z. B. Audience Manager) abgelehnt hat. </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (opt.dmp) </li> <li> ****<br/> Heartbeats: (s:meta:cm.ssf) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Inhalt </li> <li> ****<br/> Kontextdaten:Nicht zutreffend </li> <li> **Datenfeed:**<br/>video </li> <li> ****<br/> Audience Manager:Nicht zutreffend </li> </ul> |

### Ausschluss-Freigabe

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK-Schlüssel:Nicht zutreffend </li> <li> ****<br/> API-Schlüssel: analytics.optOutShare </li> <li> **Erforderlich:**<br/>nein </li> <li> ****<br/> Typ: boolean </li> <li> ****<br/> Gesendet mit: Medienstart </li> <li> **Min.** SDK-Version:Nicht zutreffend </li> <li> ****<br/> Beispielwert: true </li> <li>****<br/> Beschreibung: Auf "true"setzen, wenn der Endbenutzer sich für die Verknüpfung seiner Daten (z. B. mit anderen Adobe Analytics-Clients) entschieden hat. </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (opt.oos) </li> <li> ****<br/> Heartbeats: (s:meta:cm.oos) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>Bei BESUCH </li> <li> **Berichtsname:**<br/>Inhalt </li> <li> ****<br/> Kontextdaten:Nicht zutreffend </li> <li> **Datenfeed:**<br/>video </li> <li> ****<br/> Audience Manager:Nicht zutreffend </li> </ul> |

## Verwandte APIs {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS: [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast: [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

