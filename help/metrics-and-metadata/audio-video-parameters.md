---
title: Audio- und Videoparameter
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: ht
source-git-commit: ccd4209f6fad0547e9595674602ee978d86e10cd
workflow-type: ht
source-wordcount: '6103'
ht-degree: 100%

---


# Audio- und Videoparameter {#audio-and-video-parameters}

>[!IMPORTANT]
>
>Am 7. Februar 2019 wurde in Adobe Analytics for Video and Audio ein Metrikname geändert. <i>Medienaufrufe</i> werden nun als <i>Medienstarts</i> bezeichnet. Diese Änderung wurde vorgenommen, um die Branchenstandards bezüglich Metriken und Berichten einzuhalten und um die Metrik in Berichten problemlos identifizieren zu können.

>[!NOTE]
>
>Ab dem 13. September 2018 wurden die Bezeichnungen für einige Dimensionen, Metriken und Berichte geändert, um ein inhaltsübergreifendes Tracking von Video- und Audioanalysen zu ermöglichen. Zu den geänderten Bezeichnungen gehören: *Videoaufrufe* in *Medienaufrufe*, *Videolänge* in *Inhaltsdauer* und *Videoname* in *Inhaltsname*. Die Videoberichte in Reports and Analytics wurden aktualisiert und verwenden nun die Bezeichnung „Medien“ anstelle von „Video“. Die Änderung der Bezeichnungen hat keinen Einfluss auf die Datenerfassung oder historische Daten. Beachten Sie diese Änderungen, wenn Sie sie in Report Builder oder in anderen externen automatisierten Datenabrufen verwenden, die von dieser Änderung betroffen sein könnten.

Dieses Thema enthält eine Liste von Audio- und Videoinhaltsdaten, einschließlich Kontextdatenwerten, die Adobe über Lösungsvariablen sammelt.

Beschreibung der Tabellendaten:

* **Implementierung:** Angaben zu den Implementierungswerten und -anforderungen
   * *Schlüssel* - Variable, die entweder manuell in Ihrer App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich* - Gibt an, ob der Parameter für die algemeine Audio- und Video-Tracking erforderlich ist.
   * *Typ* - Gibt den Typ der festzulegenden Variablen an, nämlich Zeichenfolge oder Zahl.
   * *Gesendet mit* - Gibt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf beim Medienstart, *Ad Start* der Aufruf beim Anzeigenstart usw. *Close* ist der zusammengefasste Analytics-Aufruf, der am Ende der Mediensitzung oder am Ende der Anzeige, des Kapitels usw. vom Heartbeat-Server direkt an den Analytics-Server gesendet wird. Die Aufrufe zum Schließen sind in Netzwerk-Paketaufrufen nicht verfügbar.
   * *Min. SDK-Version* - Gibt an, welche SDK-Version Sie für den Zugriff auf den Parameter benötigen.
   * *Beispielwert* - Bietet ein Beispiel für die Verwendung häufiger Variablen.
* **Netzwerkparameter:** Zeigt die Werte an, die an Adobe Analytics- oder Heartbeat-Server übergeben werden. Diese Spalte enthält die Namen der Parameter, die in den von Adobe Media SDKs generierten Netzwerkaufrufen dargestellt werden.
* **Berichte:** Informationen zur Ansicht und Analyse der Audio- und Videodaten.
   * *Verfügbar* - Zeigt an, ob die Daten standardmäßig in Berichten verfügbar sind (*Ja*) oder ob eine benutzerdefinierte Einrichtung erforderlich ist (*Benutzerdefiniert*)
   * *Reservierte Variable* - Gibt an, ob die Daten als Ereignis, eVar, prop oder Klassifizierung in einer reservierten Variablen erfasst werden.
   * *Gültigkeit* - Gibt an, ob die Daten nach jedem Treffer oder nach jedem Besuch Gültigkeiten.
   * *Berichtsname* - Name des Adobe Analytics-Berichts für eine Variable
   * *Kontextdaten* - Name der Adobe Analytics-Kontextdaten, die an den Reporting-Server übergeben und in Verarbeitungsregeln verwendet werden.
   * *Daten-Feed* - Spaltenname für eine Variable in Clickstream- oder Live-Stream-Daten-Feeds
   * *Audience Manager* - Trait Name in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändern Sie nicht die Klassifizierungsnamen für Variablen, die unter Berichterstellung/Reservierte Variable als „Klassifizierung“ beschrieben sind.\
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für das Medien-Tracking aktiviert ist. Adobe fügt von Zeit zu Zeit neue Eigenschaften hinzu. In diesem Fall müssen Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften zu erhalten. Während des Aktualisierungsvorgangs ermittelt Adobe anhand der Namen der Variablen, ob die Klassifizierungen aktiviert sind. Wenn eine fehlt, fügt Adobe die fehlenden erneut hinzu.

## Core-Audio- und Videodaten {#core-audio-and-video-data}

### Streamtyp {#stream-type}

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.streamType</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 2.2 <br/><br/>Verfügbar in [Überblick über die Media Collection API](/help/media-collection-api/mc-api-overview.md) oder [SDKs herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Probenwert:**<br/> „Video“</li> <li> **Beschreibung:**<br/>Gibt den Stream-Typ an. Gültige Werte sind „audio“, „video“ und „“.<br/><br/>[Segmente für das Reporting](/help/metrics-and-metadata/segments.md):<br/><br/>Medien-Streamtyp: All -<br/>Segmentieren aller Daten des Medienstreams; Regel: Content (ID) exists<br/><br/>Medien-Streamtyp: Audio -<br/>Segmentieren aller Daten des Audiostreams; Regel: Content (ID) exists AND Media Stream Type = audio<br/><br/>Medien-Streamtyp: Video -<br/>Segmentieren aller Daten des Videostreams; Regel: Content (ID) exists AND Media Stream Type != audio<br/><br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.streamType)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.streamType)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>Bei BESUCH</li> <li> **Berichtsname:**<br/>Inhalt</li> <li> **Kontextdaten:**<br/>(a.media.streamType)</li> <li> **Daten-Feed:**<br/>videostreamtype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.streamType)</li> </ul> |

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
| <ul> <li> **SDK-Schlüssel:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.id</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „4586695ABC“</li> <li>**Beschreibung:**<br/>Inhalts-ID des Inhalts, die verwendet werden kann, um eine Verknüpfung zu anderen Branchen-/CMS-IDs herzustellen. Entspricht dem letzten Wert von`s:asset:video_id.`</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.name)</li> <li> **Heartbeat:**<br/>(s:asset:video_id)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>Bei BESUCH</li> <li> **Berichtsname:**<br/>Inhalt</li> <li> **Kontextdaten:**<br/>(a.media.name)</li> <li> **Daten-Feed:**<br/>video</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.name)</li> </ul> |

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
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.length</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> VOD: 128; Live: 86400; Linear: 1800.</li><li> **Beschreibung:**<br/>Cliplänge/Laufzeit: Die maximale Länge (oder Dauer) des wiedergegebenen Inhalts (in Sekunden). Sie entspricht dem letzten Wert von`l:asset:length`der Ereignisse des Typs „Main“.<br/>Wenn`l:asset:length`nicht festgelegt ist, wird der letzte Wert von`l:asset:duration`verwendet.<br/>Im Reporting stellt „Videolänge“ die Klassifikation und „Inhaltsdauer (Variable)“ die eVAR dar.<br/> **Wichtig:** Diese Eigenschaft wird verwendet, um verschiedene Metriken zu berechnen, z. B. Metriken für Fortschritts-Tracking und Zielgruppendurchschnitt pro Minute. Wenn sie nicht festgelegt ist oder kleiner/gleich null ist, sind diese Metriken nicht verfügbar.  Bei Live-Medien mit unbekannter Dauer wird standardmäßig der Wert „86400“ verwendet. <br/>Vor Version 1.5.1 hieß dieser Wert `l:asset:duration`. Mit Version 1.5.1 wurde er in `l:asset:length.`<br/> umbenannt. **Releasedatum: 13.09.2018** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.length)</li> <li> **Heartbeats:**<br/>(l:asset:length)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Inhaltsdauer (Variable)</li> <li> **Kontextdaten:**<br/>(a.media.length)</li> <li> **Daten-Feed:**<br/>videolength</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.length)</li> </ul> |

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
| <ul> <li> **SDK-Schlüssel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.length</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> VOD: 128; Live: 86400; Linear: 1800.</li> <li> **Beschreibung:**<br/>Cliplänge/Laufzeit: Die maximale Länge (oder Dauer) des wiedergegebenen Inhalts (in Sekunden). Sie entspricht dem letzten Wert von`l:asset:length`der Ereignisse des Typs „Main“. Wenn`l:asset:length`nicht festgelegt ist, wird der letzte Wert von`l:asset:duration`verwendet. Im Reporting stellt „Videolänge“ die Klassifikation und „Inhaltsdauer (Variable)“ die eVAR dar.<br/> **Wichtig:** Diese Eigenschaft wird verwendet, um verschiedene Metriken zu berechnen, z. B. Metriken für Fortschritts-Tracking und Zielgruppendurchschnitt pro Minute. Wenn sie nicht festgelegt ist oder kleiner/gleich null ist, sind diese Metriken nicht verfügbar.  Bei Live-Medien mit unbekannter Dauer wird standardmäßig der Wert „86400“ verwendet. Vor Version 1.5.1 hieß dieser Wert `l:asset:duration`. Mit Version 1.5.1 wurde er in `l:asset:length.`<br/> umbenannt. **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.length)</li> <li> **Heartbeats:**<br/>(l:asset:length)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Classification</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Videodauer</li> <li> **Kontextdaten:**<br/>(a.media.length)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.length)</li> </ul> |

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
| <ul> <li> **SDK-Schlüssel:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.contentType</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>beschränkte Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „vod“</li> <li> **Beschreibung:**<br/> Verfügbare Werte pro **Stream-Typ:** <br/> _Audio:_ „song“, „podcast“, „audiobook“, „radio“ <br/> _Video:_ „VoD“, „Live“, „Linear“, „UGC“, „DVoD“ <br/> Kunden können für diesen Parameter benutzerdefinierte Werte bereitstellen. Dies entspricht `s:stream:type.` Wenn dies nicht festgelegt ist, ist dies gleich `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.contentType)</li> <li> **Heartbeats:**<br/>(s:stream:type)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Content-Typ</li> <li> **Kontextdaten:**<br/>(a.contentType)</li> <li> **Daten-Feed:**<br/>videocontenttype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.contentType)</li> </ul> |

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
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>vom Backend abgerufen</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.8 </li> <li> **Beispielwert:**<br/> 1482236761294786918253</li> <li> **Beschreibung:**<br/>Identifiziert eine Instanz eines Inhalts-Streams, die für die jeweilige Wiedergabe eindeutig ist.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.vsid)</li> <li> **Heartbeat:**<br/>(s:event:sid)</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/>anwenderspezifisch</li> <li> **Kontextdaten:**<br/>(a.media.vsid)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.vsid)</li> </ul> |

### Markierung „Medien heruntergeladen“

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> `config.downloadedcontent` </li> <li> **API-Schlüssel:**<br/>vom Backend abgerufen</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>boolean</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** <br/>Starten Sie die Android- und iOS-Erweiterung 1.1.0 </li> <li> **Beispielwert:**<br/> true</li> <li> **Beschreibung:**<br/>Wird auf „true“ (wahr) gesetzt, wenn der Treffer aufgrund der Wiedergabe einer Mediensitzung mit heruntergeladenen Inhalten generiert wird. Nicht vorhanden, wenn keine heruntergeladenen Inhalte wiedergegeben werden.<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.downloaded)</li> <li> **Heartbeat:**<br/>(s:meta:a.media.downloaded)</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/>anwenderspezifisch</li> <li> **Kontextdaten:**<br/>(a.media.downloaded)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.downloaded)</li> </ul> |

### Inhalts-Player-Name

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.playerName</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „Brightcove“</li> <li> **Beschreibung:**<br/>Name des Players.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>playerName)</li> <li> **Heartbeats:**<br/>(s:sp:player_name)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Inhalts-Player-Name</li> <li> **Kontextdaten:**<br/>(a.media.playerName)</li> <li> **Daten-Feed:**<br/>videoplayername</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.playerName)</li> </ul> |

### Inhaltskanal

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.channel</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „Sports“</li> <li> **Beschreibung:**<br/>Verbreitungsstation/-kanäle oder wo der Inhalt wiedergegeben wird. Hier sind beliebige Zeichenfolgen zulässig.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.channel)</li> <li> **Heartbeats:**<br/>(s:sp:channel)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtstyp:**<br/>Inhaltskanal</li> <li> **Kontextdaten:**<br/>(a.media.channel)</li> <li> **Daten-Feed:**<br/>videochannel</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.channel)</li> </ul> |

### Inhaltssegment

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Erforderlich:**<br/>ja</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „0-10“</li> <li> **Beschreibung:**<br/>Das Intervall, das den Teil des Inhalts beschreibt, der angezeigt wurde (in Minuten). Das Segment wird als Mindest- und Höchstwert der Werte der Abspielleiste bei einer Wiedergabesitzung berechnet.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Inhaltssegment</li> <li> **Kontextdaten:**<br/>(a.media.segment)</li> <li> **Daten-Feed:**<br/>videosegment</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.segment)</li> </ul> |

### Inhaltsname (Variable)

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API-Schlüssel:**<br/>media.name</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/> „The Big Bang Theory“</li> <li> **Beschreibung:**<br/>Dies ist der (für Menschen lesbare) Anzeigename des Inhalts, der dem letzten Wert von`s:asset:name.`<br/>entspricht. In der Berichterstellung ist der Videoname die Classification und der Inhaltsname (Variable) der eVAR.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>friendlyName)</li> <li> **Heartbeats:**<br/>(s:asset:name)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Inhaltsname (Variable)</li> <li> **Kontextdaten:**<br/>(a.media.friendlyName)</li> <li> **Daten-Feed:**<br/>videoname</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.friendlyName)</li> </ul> |

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
| <ul> <li> **SDK-Schlüssel:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.name</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.1 </li> <li> **Beispielwert:**<br/> „The Big Bang Theory“</li> <li> Beschreibung:Dies ist der (für Menschen lesbare) Anzeigename des Inhalts, der dem letzten Wert von  entspricht. In Berichten ist der Videoname die Klassifizierung und der Inhaltsname (Variable) der eVAR.  **Beschreibung:**<br/>Dies ist der (für Menschen lesbare) Anzeigename des Inhalts, der dem letzten Wert von`s:asset:name.`<br/>entspricht. In Berichten ist der Videoname die Classification und der Inhaltsname (Variable) der eVAR.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>friendlyName)</li> <li> **Heartbeats:**<br/>(s:asset:name)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Classification</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Videoname</li> <li> **Kontextdaten:**<br/>(a.media.friendlyName)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.friendlyName)</li> </ul> |

### Videopfad

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „4586695ABC“</li> <li> **Beschreibung:**<br/>Bietet die Möglichkeit, den Pfad eines Betrachters über eine Site und/oder App zu verfolgen, um den Pfad anzuzeigen, den er zum Anzeigen eines bestimmten Videos eingeschlagen hat. Beliebige Integer- und/oder Buchstaben-Kombination.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.name)</li> <li> **Heartbeat:**<br/>(s:asset:video_id)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Prop</li> <li> **Berichtsname:**<br/>Videopfad</li> <li> **Kontextdaten:**<br/>(a.media.name)</li> <li> **Daten-Feed:**<br/>videopath</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.name)</li> </ul> |

### SDK-Version

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API-Schlüssel:**<br/>media.sdkVersion</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „2.62.0_release“</li> <li> **Beschreibung:**<br/>Die vom Player verwendete SDK-Version. Hier ist jeder Wert möglich, der für Ihren Player sinnvoll ist.<br/><br/>Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>sdkVersion)</li> <li> **Heartbeats:**<br/>(s:sp:sdk)</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/>(a.media.sdkVersion)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.sdkVersion)</li> </ul> |

### VHL-Version

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „js-2.0.1.88-c8c0b1“</li> <li> **Beschreibung:**<br/>Die für die Tracking-Sitzung verwendete Media SDK-Version.<br/><br/>Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.<br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.<br/>vhlVersion)</li> <li> **Heartbeats:**<br/>(s:sp:hb_version)</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/>anwenderspezifisch</li> <li> **Kontextdaten:**<br/>(a.media.vhlVersion)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.vhlVersion)</li> </ul> |

## Standard-Audio- und Videometadaten {#standard-audio-and-video-metadata}

### Show

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SHOW</li> <li> **API-Schlüssel:**<br/>media.show</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/>„Modern Family“ „The Last Dance“ „New Girl“</li> <li> **Beschreibung:**<br/>Programm-/Serienname<br/>Der Programmname ist nur erforderlich, wenn die Sendung Teil einer Serie ist.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.show)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.show)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Serie</li> <li> **Kontextdaten:**<br/>(a.media.show)</li> <li> **Daten-Feed:**<br/>videoshow</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.show)</li> </ul> |

### Stream-Format

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>STREAM_FORMAT</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „Live“</li> <li> **Beschreibung:**<br/>Format des Streams (Live, VOD, Linear).</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.format)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.format)</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/>anwenderspezifisch</li> <li> **Kontextdaten:**<br/>(a.media.format)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.format)</li> </ul> |

### Staffel

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SEASON</li> <li> **API-Schlüssel:**<br/>media.season</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „2“</li> <li> **Beschreibung:**<br/>Die Staffelnummer der Sendung.  Die Staffelserie ist nur erforderlich, wenn die Sendung Teil einer Serie ist.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.season)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.season)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Staffel</li> <li> **Kontextdaten:**<br/>(a.media.season)</li> <li> **Daten-Feed:**<br/>videoseason</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.season)</li> </ul> |

### Episode

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>EPISODE</li> <li> **API-Schlüssel:**<br/>media.episode</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „13“</li> <li> **Beschreibung:**<br/>Die Nummer der Folge.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.episode)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.episode)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Episode</li> <li> **Kontextdaten:**<br/>(a.media.episode)</li> <li> **Daten-Feed:**<br/>videoepisode</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.episode)</li> </ul> |

### Element-ID

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ASSET_ID</li> <li> **API-Schlüssel:**<br/>media.assetId</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „89745363“</li> <li> **Beschreibung:**<br/>Die eindeutige ID für den Inhalt des Medien-Assets, z. B. die Kennung einer Serienfolge, eines Film-Assets oder eines Live-Events. Normalerweise stammen diese IDs von Metadatensystemen wie EIDR, TMS/Gracenote oder Rovi. Diese Kennungen können auch von anderen proprietären oder internen Systemen stammen.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.asset)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.asset)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Classification</li> <li> **Berichtsname:**<br/>Asset-ID</li> <li> **Kontextdaten:**<br/>(a.media.asset)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.asset)</li> </ul> |

### Genre

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>GENRE</li> <li> **API-Schlüssel:**<br/>media.genre</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „Drama“, „Comedy“</li> <li> **Beschreibung:**<br/>Typ oder Gruppe des Inhalts nach Definition des Inhaltserstellers. Werte sollten bei der Variablenimplementierung durch Kommata getrennt sein. In Berichten unterteilt das Listen-eVar jeden Wert in einen Zeileneintrag, wobei jeder Zeileneintrag die gleiche Gewichtung erhält.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.genre)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.genre)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Listen-eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Genre</li> <li> **Kontextdaten:**<br/>(a.media.genre)</li> <li> **Daten-Feed:**<br/>videogenre</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.genre)</li> </ul> |

### Erstes Sendedatum

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FIRST_AIR_DATE</li> <li> **API-Schlüssel:**<br/>media.firstAirDate</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „2016-01-25“</li> <li> **Beschreibung:**<br/>Das Datum der Erstausstrahlung des Inhalts im Fernsehen. Hier kann jedes Datumsformat verwendet werden, jedoch empfiehlt Adobe JJJJ-MM-TT.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.airDate)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.airDate)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Classification</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Erstes Sendedatum</li> <li> **Kontextdaten:**<br/>(a.media.airDate)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.airDate)</li> </ul> |

### Erstes digitales Veröffentlichungsdatum

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FIRST_DIGITAL_DATE</li> <li> **API-Schlüssel:**<br/>media.firstDigitalDate</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „2016-01-25“</li> <li> **Beschreibung:**<br/>Das Datum der Erstausstrahlung des Inhalts auf einem digitalen Kanal oder einer digitalen Plattform. Hier kann jedes Datumsformat verwendet werden, jedoch empfiehlt Adobe JJJJ-MM-TT.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.digitalDate)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.digitalDate)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Classification</li> <li> **Berichtsname:**<br/>Erstes digitales Veröffentlichungsdatum</li> <li> **Kontextdaten:**<br/>(a.media.digitalDate)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.digitalDate)</li> </ul> |

### Inhaltsbewertung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>RATING</li> <li> **API-Schlüssel:**<br/>media.rating</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> TVY, TVG, TVPG, TVMA</li> <li> **Beschreibung:**<br/>Die Alterseinstufung nach Definition von TV Parental Guidelines.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.rating)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.rating)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Classification</li> <li> **Berichtsname:**<br/>Inhaltsbewertung</li> <li> **Kontextdaten:**<br/>(a.media.rating)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.rating)</li> </ul> |

### Urheber

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>ORIGINATOR</li> <li> **API-Schlüssel:**<br/>media.originator</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „Warner Brothers“, „Sony“, „Disney“</li> <li> **Beschreibung:**<br/>Der Ersteller des Inhalts.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.originator)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.originator)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Classification</li> <li> **Berichtsname:**<br/>Urheber</li> <li> **Kontextdaten:**<br/>(a.media.originator)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.originator)</li> </ul> |

### Netzwerk

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>NETWORK</li> <li> **API-Schlüssel:**<br/>media.network</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „Fox“, „Bravo“, „ESPN“</li> <li> **Beschreibung:**<br/>Der Name des Netzwerks/Kanals/Senders.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.network)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.network)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Netzwerk</li> <li> **Kontextdaten:**<br/>(a.media.network)</li> <li> **Daten-Feed:**<br/>videonetwork</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.network)</li> </ul> |

### Sendungstyp

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>SHOW_TYPE</li> <li> **API-Schlüssel:**<br/>media.showType</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „0“ = vollständige Folge; „1“ = Vorschau/Trailer; „2“ = Clip; „3“ = Sonstiges.</li> <li> **Beschreibung:**<br/>Der Inhaltstyp, angegeben als Integer-Wert zwischen 0 und 3.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.type)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.type)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Serientyp</li> <li> **Kontextdaten:**<br/>(a.media.type)</li> <li> **Daten-Feed:**<br/>videoshowtype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.type)</li> </ul> |

### MVPD

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>MVPD</li> <li> **API-Schlüssel:**<br/>media.pass.mvpd</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „Comcast“, „DirecTV“, „Dish“</li> <li> **Beschreibung:**<br/>Über Adobe-Authentifizierung bereitgestellter MVPD.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.pass.mvpd)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.pass.<br/>mvpd)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>MVPD</li> <li> **Kontextdaten:**<br/>(a.media.pass.mvpd)</li> <li> **Daten-Feed:**<br/>videomvpd</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pass.mvpd)</li> </ul> |

### Autorisiert

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>AUTHORIZED</li> <li> **API-Schlüssel:**<br/>media.pass.auth</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „TRUE“</li> <li> **Beschreibung:**<br/>Der Benutzer wurde über die Adobe-Authentifizierung autorisiert.<br/>**Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.pass.auth)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.pass.<br/>auth)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Autorisiert</li> <li> **Kontextdaten:**<br/>(a.media.pass.auth)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pass.auth)</li> </ul> |

### Tagesteil

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>DAY_PART</li> <li> **API-Schlüssel:**<br/>media.dayPart</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> </li> <li> **Beschreibung:**<br/>Eine Eigenschaft, die die Tageszeit definiert, zu der der Inhalt ausgestrahlt oder wiedergegeben wurde. Hier können Kunden jeden erforderlichen Wert festlegen.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.dayPart)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.dayPart)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Tagesteil</li> <li> **Kontextdaten:**<br/>(a.media.dayPart)</li> <li> **Daten-Feed:**<br/>videodaypart</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.dayPart)</li> </ul> |

### Medien-Feed-Typ

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>FEED</li> <li> **API-Schlüssel:**<br/>media.feed</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 </li> <li> **Beispielwert:**<br/> „East-HD“, „West-HD“, „East-SD“</li> <li> **Beschreibung:**<br/>Die Art des Feeds.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.feed)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.feed)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/>Medien-Feed-Typ</li> <li> **Kontextdaten:**<br/>(a.media.feed)</li> <li> **Daten-Feed:**<br/>videofeedtype</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.feed)</li> </ul> |

### Künstler

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.artist</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 <br/>Verfügbar in [Überblick über die Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder [SDKs herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/> „Die Beatles“</li> <li> **Beschreibung:**<br/>Name des Künstlers.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.artist)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.artist)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/>(a.media.artist)</li> <li> **Daten-Feed:**<br/>videoaudioartist</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.artist)</li> </ul> |

### Album

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.album</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 <br/>Verfügbar in [Überblick über die Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder [SDKs herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/> „Revolver“</li> <li> **Beschreibung:**<br/>Name des Albums.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.album)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.album)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/>(a.media.album)</li> <li> **Daten-Feed:**<br/>videoaudioalbum</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.album)</li> </ul> |

### Beschriftung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.label</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 <br/>Verfügbar in [Überblick über die Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder [SDKs herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/> „Revolver“</li> <li> **Beschreibung:**<br/>Name des Plattenlabels.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.label)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.label)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/>(a.media.label)</li> <li> **Daten-Feed:**<br/>videoaudiolabel</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.label)</li> </ul> |

### Autor

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.author</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 <br/>Verfügbar in [Überblick über die Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder [SDKs herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/> „John Kennedy Toole“</li> <li> **Beschreibung:**<br/>Name des Autors (eines Hörbuchs).<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.author)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.author)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/>(a.media.author)</li> <li> **Daten-Feed:**<br/>videoaudioauthor</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.author)</li> </ul> |

### Station

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.station</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 <br/>Verfügbar in [Überblick über die Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder [SDKs herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/> „NPR“</li> <li> **Beschreibung:**<br/>Name/ID des Radiosenders.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.station)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.station)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/>(a.media.station)</li> <li> **Daten-Feed:**<br/>videoaudiostation</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.station)</li> </ul> |

### Publisher

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.publisher</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start, Media Close</li> <li> **Min. SDK-Version:** 1.5.7 <br/>Verfügbar in [Überblick über die Mediensammlung](/help/media-collection-api/mc-api-overview.md) oder [SDKs herunterladen - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Beispielwert:**<br/> „Random Bauhaus“</li> <li> **Beschreibung:**<br/>Name des Herausgebers des Audioinhalts.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.publisher)</li> <li> **Heartbeats:**<br/>(s:meta:<br/>a.media.publisher)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>bei HIT</li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/>(a.media.publisher)</li> <li> **Daten-Feed:**<br/>videoaudiopublisher</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.publisher)</li> </ul> |

## Audio- und Videometriken {#audio-and-video-metrics}

### Medienstarts

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Start</li> <li> **Min. SDK-Version:** beliebig</li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Ladeereignis für das Medium. (Tritt auf, wenn der Zuschauer auf die_Play _-Schaltfläche klickt). Gilt auch, wenn Pre-Roll-Anzeigen, Puffern, Fehler usw. auftreten.<br/>**Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.view)</li> <li> **Heartbeats:**<br/>(s:event:<br/>type=start)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtname:**<br/>Medienstarts</li> <li> **Kontextdaten:**<br/>(a.media.view)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.view)</li> </ul> |

### Inhaltsstarts

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Der erste Frame des Mediums wird wiedergegeben. Wenn der Anwender den Inhalt während einer Anzeige, eines Puffervorgangs usw. verlässt, tritt kein Content Start-Ereignis auf.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Inhaltsstarts</li> <li> **Kontextdaten:**<br/>(a.media.play)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.play)</li> </ul> |

### Inhaltsbeendigung {#content-complete}

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Ein Stream, der bis zum Ende angesehen wurde. Dies bedeutet nicht unbedingt, dass der Benutzer den gesamten Stream gesehen oder angehört hat. Sie hätten vorausspringen können. Dies bedeutet nur, dass der Benutzer das Ende des Streams zu 100% erreicht hat.<br/>Siehe auch[Sitzungsende](quality-parameters.md#session-end)<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>(s:event:<br/>type=complete)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Inhaltsbeendigungen</li> <li> **Kontextdaten:**<br/>(a.media.complete)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.complete)</li> </ul> |

### Inhaltsbesuchszeit

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 105</li> <li> **Beschreibung:**<br/> Addiert die Ereignisdauer (in Sekunden) für alle Ereignisse des Typs „PLAY“ im Hauptinhalt.  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Daten-Feeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Besuchszeit für Inhalt</li> <li> **Kontextdaten:**<br/>(a.media.timePlayed)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.timePlayed)</li> </ul> |

### Besuchszeit für Medien

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 120</li> <li> **Beschreibung:**<br/>Addiert die Ereignisdauer (in Sekunden) für alle Ereignisse des Typs „PLAY“ in Haupt- und Anzeigeninhalt.  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Daten-Feeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Besuchszeit für Medien</li> <li> **Kontextdaten:**<br/>(a.media.totalTimePlayed)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.totalTimePlayed)</li> </ul> |

### Eindeutige Spielzeit

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 94</li> <li> **Beschreibung:**<br/>Der Wert in Sekunden für die einzelnen Segmente des Inhalts, die während einer Sitzung abgespielt werden. Ausgenommen sind Szenarios mit Suchvorgängen, in denen ein Betrachter das gleiche Segment des Inhalts mehrmals betrachtet.  Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Daten-Feeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>anwenderspezifisch</li> <li> **Kontextdaten:**<br/>(a.media.uniqueTimePlayed)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.uniqueTimePlayed)</li> </ul> |

### 10 %-Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Die Abspielleiste überspringt die 10 %-Markierung basierend auf der Inhaltsdauer. Die Markierung wird nur einmal gezählt, selbst wenn der Benutzer zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>10 % Fortschrittsmarkierung</li> <li> **Kontextdaten:**<br/>(a.media.progress10)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress10)</li> </ul> |

### 25 %-Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Die Abspielleiste überspringt die 25%-Markierung basierend auf der Inhaltsdauer. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>25 % Fortschrittsmarkierung</li> <li> **Kontextdaten:**<br/>(a.media.progress25)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress25)</li> </ul> |

### 50 %-Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Die Abspielleiste überspringt die 50%-Markierung basierend auf der Inhaltsdauer. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>50 % Fortschrittsmarkierung</li> <li> **Kontextdaten:**<br/>(a.media.progress50)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress50)</li> </ul> |

### 75 %-Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/> **Nicht zutreffend** </li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Die Abspielleiste überspringt die 75%-Markierung basierend auf der Inhaltsdauer. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>75 % Fortschrittsmarkierung</li> <li> **Kontextdaten:**<br/>(a.media.progress75)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress75)</li> </ul> |

### 95 %-Fortschrittsmarkierung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Die Abspielleiste überspringt die 95%-Markierung basierend auf der Inhaltsdauer. Die Markierung wird nur einmal gezählt, selbst wenn der Anwender zu einer früheren Abspielposition springt. Springt er zu einer späteren Abspielposition, werden hierbei übersprungene Markierungen nicht gewertet.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>95 % Fortschrittsmarkierung</li> <li> **Kontextdaten:**<br/>(a.media.progress95)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.progress95)</li> </ul> |

### Zielgruppendurchschnitt pro Minute

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> Größer als oder gleich 1</li> <li> **Beschreibung:**<br/>Die Metrik „Zielgruppendurchschnitt pro Minute“ wird berechnet, indem die Gesamtbesuchszeit für den Inhalt eines bestimmten Mediums durch die Länge dieses Mediums für alle zugehörigen Wiedergabesitzungen geteilt wird:<br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Zielgruppendurchschnitt pro Minute</li> <li> **Kontextdaten:**<br/>(a.media.averageMinuteAudience)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.averageMinuteAudience)</li> </ul> |

### Sekunden seit dem letzten Aufruf

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 600</li> <li> **Beschreibung:**<br/>Die Sekunden seit dem letzten Aufruf sind 0, wenn der Stream mit einem vollständigen Ereignis oder mit einem Endereignis geschlossen wurde, und normalerweise 600, wenn er aufgrund eines Timeouts geschlossen wurde. Für diese Metrik gibt es keine Lösungsvariable und keine Regeln für die automatische Verarbeitung. Daher müssen Sie eine benutzerspezifische Verarbeitungsregel erstellen, um sie zu speichern.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/>nicht verfügbar</li> <li> **Kontextdaten:**<br/>(a.media.secondsSinceLastCall)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.secondsSinceLastCall)</li> </ul> |

### Verknüpfte Daten

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>boolean</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> true</li> <li> **Beschreibung:**<br/>Wird auf „true“ (wahr) gesetzt, wenn der Treffer verknüpft ist (daher, vom Kunden als Teil einer verknüpften Datenfreigabe empfangen wird und nicht als eigene Implementierung).</li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/>nicht verfügbar</li> <li> **Kontextdaten:**<br/>(a.media.federated)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.federated)</li> </ul> |

### Geschätzte Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 - 19-minütige Wiedergabe;<br/>2 - 31-minütige Wiedergabe;<br/>3 - 78-minütige Wiedergabe.</li> <li> **Beschreibung:**<br/>Die geschätzte Anzahl von Video- oder Audio-Streams pro jeweiligem Inhalt. Dieser Wert wird je 30 Minuten Wiedergabezeit (Inhalt und Anzeigen) erhöht. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.<br/><br/>Ein Stream wird alle 30 Minuten gezählt, basierend auf`ms_s`(oder totalTimePlayed = Gesamtvideozeit), ähnlich wie:<br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel.</li> <li> **Reservierte Variable:**<br/>nicht verfügbar</li> <li> **Berichtsname:**<br/>anwenderspezifisch</li> <li> **Kontextdaten:**<br/>(a.media.estimatedStreams)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.estimatedStreams)</li> </ul> |

### Betroffene Streams pausiert

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Dieser Wert ist entweder „true“ oder „false“. Er ist „true“, wenn während der Wiedergabe eines einzelnen Mediums mindestens eine Pause auftritt.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>(s:event:<br/>type=pause)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Betroffene Streams pausiert</li> <li> **Kontextdaten:**<br/>(a.media.pause)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pause)</li> </ul> |

### Pausierung – Ereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/> 2</li> <li> **Beschreibung:**<br/>Diese Metrik wird als Anzahl der Pausenperioden berechnet, die während einer Wiedergabesitzung aufgetreten sind.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>(s:event:<br/>type=pause)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Pausierung – Ereignisse</li> <li> **Kontextdaten:**<br/>(a.media.pauseCount)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pauseCount)</li> </ul> |

### Pausierung – Gesamtdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zahl</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/> 190</li> <li> **Beschreibung:**<br/>Addiert die Dauer (in Sekunden) aller Ereignisse des Typs „PAUSE“. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Daten-Feeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.<br/> **Releasedatum: 13.09.2018** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Pausierung – Gesamtdauer</li> <li> **Kontextdaten:**<br/>(a.media.pauseTime)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.pauseTime)</li> </ul> |

### Inhaltswiederaufnahmen

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/> **media.resume** </li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** 1.5.6 </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Eine Wiederaufnahme wird für jede Wiedergabe gezählt, die nach mehr als 30 Minuten Pufferzeit, Pausierung oder Unterbrechung fortgesetzt wird, ODER wenn dieser Wert vom Player im VideoInfo-Objekt trackPlay festgelegt wird.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>(s:event:<br/>type=resume)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Inhaltswiederaufnahmen</li> <li> **Kontextdaten:**<br/>(a.media.resume)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.resume)</li> </ul> |

### Ansichten des Inhaltssegments

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt</li> <li> **API-Schlüssel:**<br/>nicht verfügbar</li> <li> **Typ:**<br/>Zeichenfolge</li> <li> **Gesendet mit:**<br/>Media Close</li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE</li> <li> **Beschreibung:**<br/>Die Anzahl der Aufrufe des Hauptinhalts. Eine Inhaltssegmentansicht wird gezählt, wenn mindestens ein Bild angezeigt wurde.<br/> **Wichtig:** Ist dieser Wert festgelegt, kann er nur „true“ lauten. Ist er nicht festgelegt, wird kein Wert zurückgegeben. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar</li> <li> **Heartbeats:**<br/>nicht verfügbar</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>Ereignis</li> <li> **Berichtsname:**<br/>Ansichten des Inhaltssegments</li> <li> **Kontextdaten:**<br/>(a.media.segmentView)</li> <li> **Daten-Feed:**<br/>nicht verfügbar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.segmentView)</li> </ul> |

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

### Ablehnen der serverseitigen Weiterleitung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>nicht zutreffend</li> <li> **API-Schlüssel:**<br/>analytics.optOutServerSideForwarding</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>boolean</li> <li> **Gesendet mit:**<br/>Media Start</li> <li> **Min. SDK-Version:** nicht zutreffend </li> <li> **Beispielwert:**<br/> true</li> <li>**Beschreibung:**<br/>Wird auf „true“ (wahr) gesetzt, wenn der Endbenutzer die Freigabe seiner Daten für Adobe Analytics und andere Experience Cloud-Lösungen (z. B. Audience Manager) abgelehnt hat.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(opt.dmp)</li> <li> **Heartbeats:**<br/>(s:meta:cm.ssf)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>Bei BESUCH</li> <li> **Berichtsname:**<br/>Inhalt</li> <li> **Kontextdaten:**<br/>Nicht zutreffend</li> <li> **Daten-Feed:**<br/>video</li> <li> **Audience Manager:**<br/>Nicht zutreffend</li> </ul> |

### Ablehnen der Freigabe

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>nicht zutreffend</li> <li> **API-Schlüssel:**<br/>analytics.optOutShare</li> <li> **Erforderlich:**<br/>nein</li> <li> **Typ:**<br/>boolean</li> <li> **Gesendet mit:**<br/>Media Start</li> <li> **Min. SDK-Version:** nicht zutreffend </li> <li> **Beispielwert:**<br/> true</li> <li>**Beschreibung:**<br/>Wird auf „true“ (wahr) gesetzt, wenn der Endbenutzer die Verknüpfung seiner Daten (z. B. mit anderen Adobe Analytics-Clients) abgelehnt hat.</li></ul> | <ul> <li> **Adobe Analytics:**<br/>(opt.oos)</li> <li> **Heartbeats:**<br/>(s:meta:cm.oos)</li> </ul> | <ul> <li> **Verfügbar:**<br/>ja</li> <li> **Reservierte Variable:**<br/>eVar</li> <li> **Gültigkeit:**<br/>Bei BESUCH</li> <li> **Berichtsname:**<br/>Inhalt</li> <li> **Kontextdaten:**<br/>Nicht zutreffend</li> <li> **Daten-Feed:**<br/>video</li> <li> **Audience Manager:**<br/>Nicht zutreffend</li> </ul> |

## Verwandte APIs {#section_Related_APIs}

### createMediaObject-APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig-APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)
