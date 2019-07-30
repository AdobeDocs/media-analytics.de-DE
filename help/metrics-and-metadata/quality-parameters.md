---
seo-title: Qualitätsparameter
title: Qualitätsparameter
uuid: 0 d 9 fa 764-edef -4178-8650-90 c 9 a 0852 a 57
translation-type: tm+mt
source-git-commit: 6e6ecdcb7309e06410a443247df5d5b49b083ea7

---


# Qualitätsparameter{#quality-parameters}

Dieses Thema enthält eine Liste der Qualitätsdaten (QoE/QoS), einschließlich Kontextdatenwerten, die Adobe über Lösungsvariablen erfasst.

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
   * *Audience Manager:* Eigenschaftsname in Adobe Audience Manager.

## Qualitätsmetadaten {#section_8467F9729DA04A888A2657712234D7C7}

### Durchschnittliche Bitrate

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/>media.qoe.bitrate </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 800-899 </li><li> **Beschreibung:**<br/>Die durchschnittliche Bitrate (in Kbit/s). Der Wert besteht aus vordefinierten Gruppen mit Intervallen von 100 Kbit/s. Die durchschnittliche Bitrate wird als gewichteter Durchschnitt aller Bitratenwerte im Zusammenhang mit der Wiedergabedauer berechnet, die während einer Wiedergabesitzung aufgetreten sind..  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Heartbeat:**<br/> (l: stream: Bitrate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Durchschnittliche Bitrate </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Datenfeed:**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaveragebucket) </li> </ul> |



### Zeit bis Start

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.qoe.timeToStart </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 30.000 </li><li> **Beschreibung:**<br/>Dieser Wert wird standardmäßig null, wenn Sie ihn nicht durch qosobject festlegen. Sie stellen diesen Wert in Millisekunden ein. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: stream: startup_ time) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Zeit bis Start </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Datenfeed:**<br/>videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.qoe.framesPerSecond </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medienstart, Medienschließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 24 </li><li> **Beschreibung:**<br/>Der aktuelle Wert der Stream-Framerate (in Bildern pro Sekunde).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> (l: stream: fps) </li> </ul> | <ul> <li> **Verfügbar:**<br/>nein </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> </li> <li> **Datenfeed:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Dropped Frames

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>droppedFrames </li> <li> **API-Schlüssel:**<br/>media.qoe.droppedFrames </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 3 </li><li> **Beschreibung:**<br/>Die Anzahl der Dropped Frames (Int). Dieser Wert wird als Summe aller Dropped Frames berechnet, die während einer Wiedergabesitzung aufgetreten sind. Dieser Wert wird vom letzten Wert von (l: stream: dropped_ frames).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Dropped Frames </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Datenfeed:**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Pufferereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 2 </li><li> **Beschreibung:**<br/>Die Anzahl der Pufferereignisse. Diese Metrik wird als Anzahl der verschiedenen Pufferereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind. So wird festgehalten, wie oft der Player aus anderen Status, z. B. Wiedergabe oder Pause, in einen Pufferstatus übergegangen ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = buffer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Pufferereignisse </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Datenfeed:**<br/>videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Gesamtpufferdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** </li> <li> **Beispielwert:**<br/> 30 </li><li> **Beschreibung:**<br/>Die Gesamtdauer in Sekunden, die Pufferung ausgegeben hat. Dieser Wert wird als Summe aller Pufferereignis-Zeitspannen berechnet, die während einer Wiedergabesitzung aufgetreten sind. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: Ereignis: Dauer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Gesamtpufferdauer </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Datenfeed:**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Bitratenänderungen

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.qoe.bitrateChange </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 3 </li><li> **Beschreibung:**<br/>Die Anzahl der Bitratenänderungen (Integer). Dieser Wert wird als Summe aller Bitratenänderungs-Ereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Bitratenänderungen </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Datenfeed:**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Fehler/Fehlerereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Die Anzahl der aufgetretenen Fehler (Integer). Dieser Wert wird als Summe aller Fehlerereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Datenfeed:**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### Player SDK Fehler-IDs

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die eindeutigen Fehler-IDs, die vom Player-SDK generiert wurden. Der Kunde muss die Fehlercodes/-IDs zur Implementierungszeit über die bereitgestellten Fehler-APIs bereitstellen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Datenfeed:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Playersdkerrors) </li> </ul> |



### Externe Fehler-IDs

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die eindeutigen Fehler-IDs aus beliebigen externen Quellen, z. B. CDN-Fehler. Der Kunde muss die Fehlercodes/-IDs zur Implementierungszeit über die bereitgestellten Fehler-APIs bereitstellen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Datenfeed:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Externalerrors) </li> </ul> |



### Medien-SDK Fehler-IDs

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die eindeutigen Fehler-IDs, die vom Media SDK während der Wiedergabe generiert wurden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Datenfeed:** <br/>mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Mediasdkerrors) </li> </ul> |




### Sitzungsende {#session-end}

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 2.1 </li> <li> **Beispielwert:**<br/> end </li><li> **Beschreibung:**<br/>Das end-Ereignis bedeutet, dass das SDK einen close-Aufruf an den Backend sendet. Bei Empfang dieses Ereignisses schließt das Backend die Sitzung für dieses Video und führt keine weitere Verarbeitung durch. <br/>Wenn das Medium auf 100% abgeschlossen wurde, sollte dies nach `s:event:type=complete.` dem Anzeigen [von Content Complete](audio-video-parameters.md#content-complete) für zugehörige Informationen gesendet werden. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/> (s: Ereignis: type = end) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> </li> <li> **Datenfeed:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Qualitätsmetriken {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### Zeit bis Start

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 30.000 </li><li> **Beschreibung:**<br/>Dieser Wert wird standardmäßig null, wenn Sie ihn nicht durch qosobject festlegen. Sie stellen diesen Wert in Millisekunden ein. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: stream: startup_ time) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Zeit bis Start </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Datenfeed:**<br/>videoqoetimetostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### Pufferereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 2 </li><li> **Beschreibung:**<br/>Die Anzahl der Pufferereignisse (Integer). Diese Metrik wird als Anzahl der Pufferereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = buffer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Pufferereignisse </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Datenfeed:**<br/>videoqoebuffercount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Gesamtpufferdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 15 </li><li> **Beschreibung:**<br/>Die Gesamtdauer der Pufferung (Sekunden; Ganzzahl). Dieser Wert wird als Summe aller Pufferereignis-Zeitspannen berechnet, die während einer Wiedergabesitzung aufgetreten sind. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: Ereignis: Dauer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Gesamtpufferdauer </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Datenfeed:**<br/>videoqoebuffertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Bitratenänderungen

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Ereignis </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> " 3 " </li><li> **Beschreibung:**<br/>Die Anzahl der Bitratenänderungen. Dieser Wert wird als Summe aller Bitratenänderungs-Ereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Bitratenänderungen </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Datenfeed:**<br/>videoqoebitratechangecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Fehler

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Die Anzahl der aufgetretenen Fehler (Integer). Dieser Wert wird als Summe aller Fehlerereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Fehlerereignisse </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Datenfeed:**<br/>videoqoeerrorcount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### Dropped Frames

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Die Anzahl der Dropped Frames (Integer). Dieser Wert wird als Summe aller Dropped Frames berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Dropped Frames </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Datenfeed:**<br/>videoqoedroppedframecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Drops vor Start

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Frequenz, mit der ein Benutzer das Video vor dem Start beendet. Diese Metrik wird auf 1 gesetzt, wenn kein Inhalt gerendert wurde, unabhängig von Werbeanzeigen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = aa_ start) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Drops vor Start </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Datenfeed:**<br/>videoqoedropbeforestart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Dropbeforestart) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis festgelegt ist, ist der einzige mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Puffer betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der durch Pufferung betroffenen Streams. Diese Metrik wird auf 1 gesetzt, wenn mindestens ein Pufferereignis während einer Wiedergabesitzung aufgetreten ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = buffer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Von Puffer betroffene Streams </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Datenfeed:**<br/>videoqoebuffer </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis festgelegt ist, ist der einzige mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Bitratenänderung betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams, in denen Bitratenänderungen aufgetreten sind. Diese Metrik wird auf 1 gesetzt, wenn mindestens ein Bitratenänderungs-Ereignis während einer Wiedergabesitzung aufgetreten ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> Von Bitratenänderungen betroffene Streams </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Datenfeed:**<br/>videoqoebitratechange </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechange) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis festgelegt ist, ist der einzige mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Durchschnittliche Bitrate

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 3200 </li><li> **Beschreibung:**<br/>Die durchschnittliche Bitrate (in Kbit/s, Ganzzahl). Diese Metrik wird als gewichteter Durchschnitt aller Bitratenwerte im Zusammenhang mit der Wiedergabedauer berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Heartbeat:**<br/> (l: stream: Bitrate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Durchschnittliche Bitrate </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Datenfeed:**<br/>videoqoebitrateaverage </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaverage) </li> </ul> |



### Von Fehlern betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams, in denen ein Fehlerereignis aufgetreten ist (d. h. `trackError` während der Wiedergabesitzung aufgerufen wurde und ein `type=error` Heartbeat-Aufruf generiert wurde). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>error) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Von Fehlern betroffene Streams </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>error) </li> <li> **Datenfeed:**<br/>videoqoeerror </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis festgelegt ist, ist der einzige mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Dropped Frames betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams, in denen Bilder abgelegt wurden. Diese Metrik wird auf 1 gesetzt, wenn mindestens ein Dropped Frame während einer Wiedergabesitzung aufgetreten ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Von Dropped Frames betroffene Streams </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Datenfeed:**<br/>videoqoedroppedframes </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis festgelegt ist, ist der einzige mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Unterbrechung betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5 (oder höher) </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams, in denen ein angehaltenes Ereignis aufgetreten ist. Diese Metrik wird auf 1 gesetzt, wenn während der Wiedergabe mindestens ein Unterbrechungsereignis aufgetreten ist. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = stall) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis festgelegt ist, ist der einzige mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Unterbrechungsereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5 (oder höher) </li> <li> **Beispielwert:**<br/> " 3 " </li><li> **Beschreibung:**<br/>Die Frequenz, mit der die Wiedergabe während einer Wiedergabesitzung angehalten wurde. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = stall) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stallcount) </li> </ul> |



### Gesamt-Unterbrechungsdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung   |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Medien schließen </li> <li> **Min. SDK-Version:** 1.5 (oder höher) </li> <li> **Beispielwert:**<br/> 12 </li><li> **Beschreibung:**<br/>Die Gesamtdauer (Sekunden; integer) Die Wiedergabe wurde während einer Wiedergabesitzung angehalten. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Heartbeat:**<br/> (s: Ereignis:<br/>type = stall) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stalltime) </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

