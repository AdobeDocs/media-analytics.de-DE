---
title: Qualitätsparameter
description: null
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Qualitätsparameter {#quality-parameters}

Dieses Thema enthält eine Liste der Qualitätsdaten (QoE/QoS), einschließlich Kontextdatenwerten, die Adobe über Lösungsvariablen erfasst.

Beschreibung der Tabellendaten:

* **Implementierung:** Informationen zu Implementierungswerten und -anforderungen.
   * *Schlüssel:* Variable, die entweder manuell in der App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich:* Gibt an, ob der Parameter für das Basis-Video-Tracking erforderlich ist.
   * *Typ:* Gibt den Typ der Variablen (Zeichenfolge oder Zahl) an.
   * *Gesendet mit*: Gibt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf beim Medienstart, *Ad Start* der Aufruf beim Anzeigenstart usw. *Close* ist der zusammengefasste Analytics-Aufruf, der am Ende der Mediensitzung oder am Ende der Anzeige, des Kapitels usw. vom Heartbeat-Server direkt an den Analytics-Server gesendet wird. Die Aufrufe zum Schließen sind in Netzwerk-Paketaufrufen nicht verfügbar.
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

## Qualitätsmetadaten {#quality-metadata}

### Durchschnittliche Bitrate

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/>media.qoe.bitrate </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/>Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 800-899 </li><li> **Beschreibung:**<br/>Die durchschnittliche Bitrate (in Kbit/s). Der Wert besteht aus vordefinierten Gruppen mit Intervallen von 100 Kbit/s. Die durchschnittliche Bitrate wird als gewichteter Durchschnitt aller Bitratenwerte im Zusammenhang mit der Wiedergabedauer berechnet, die während einer Wiedergabesitzung aufgetreten sind..  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Heartbeat:**<br/> (l:stream:bitrate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Durchschnittliche Bitrate </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Datenfeed:**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |


### Zeit bis Start

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.qoe.timeToStart </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 30.000 </li><li> **Beschreibung:**<br/>Dieser Wert wird standardmäßig auf 0 festgelegt, wenn Sie ihn nicht über das QoSObject einstellen. Sie stellen diesen Wert in Millisekunden ein. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l:stream:startup_time) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Zeit bis Start </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Datenfeed:**<br/>videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |


### FPS

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.qoe.framesPerSecond </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Start, Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 24 </li><li> **Beschreibung:**<br/>Der aktuelle Wert der Stream-Framerate in Frames pro Sekunde (FPS).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> (l:stream:fps) </li> </ul> | <ul> <li> **Verfügbar:**<br/>nein </li> <li> **Reservierte Variable:**<br/>nicht verfügbar </li> <li> **Berichtsname:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Dropped Frames

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>droppedFrames </li> <li> **API-Schlüssel:**<br/>media.qoe.droppedFrames </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 3 </li><li> **Beschreibung:**<br/>Die Anzahl der Dropped Frames (Integer). Dieser Wert wird als Summe aller Dropped Frames berechnet, die während einer Wiedergabesitzung aufgetreten sind. Dieser Wert wird aus dem letzten Wert von (l:stream:dropped_frames) entnommen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Dropped Frames </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Datenfeed:**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Pufferereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 2 </li><li> **Beschreibung:**<br/>Die Anzahl der Pufferereignisse. Diese Metrik wird als Anzahl der verschiedenen Pufferereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind. So wird festgehalten, wie oft der Player aus anderen Status, z. B. Wiedergabe oder Pause, in einen Pufferstatus übergegangen ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Pufferereignisse </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Datenfeed:**<br/>videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Gesamtpufferdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** </li> <li> **Beispielwert:**<br/> 30 </li><li> **Beschreibung:**<br/>Die Gesamtdauer der Pufferung (in Sekunden). Dieser Wert wird als Summe aller Pufferereignis-Zeitspannen berechnet, die während einer Wiedergabesitzung aufgetreten sind. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Heartbeat:**<br/> (l:event:duration) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Gesamtpufferdauer </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Datenfeed:**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Bitratenänderungen

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/>media.qoe.bitrateChange </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 3 </li><li> **Beschreibung:**<br/>Die Anzahl der Bitratenänderungen (Integer). Dieser Wert wird als Summe aller Bitratenänderungs-Ereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Bitratenänderungen </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Datenfeed:**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Fehler/Fehlerereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/> </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Die Anzahl der aufgetretenen Fehler (Integer). Dieser Wert wird als Summe aller Fehlerereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Datenfeed:**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Player SDK Fehler-IDs

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die vom Player-SDK generierten eindeutigen Fehler-IDs. Der Kunde muss die Fehlercodes/-IDs zur Implementierungszeit über die bereitgestellten Fehler-APIs bereitstellen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Daten-Feed:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### Externe Fehler-IDs

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die eindeutigen Fehler-IDs aus einer beliebigen externen Quelle, z. B. CDN-Fehler. Der Kunde muss die Fehlercodes/-IDs zur Implementierungszeit über die bereitgestellten Fehler-APIs bereitstellen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Daten-Feed:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### Medien-SDK Fehler-IDs

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> </li><li> **Beschreibung:**<br/>Die eindeutigen Fehler-IDs, die vom Media SDK während der Wiedergabe generiert werden.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>eVar </li> <li> **Ablauf:**<br/>bei HIT </li> <li> **Berichtsname:**<br/>Fehler </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Datenfeed:** <br/>mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul> |




### Sitzungsende {#session-end}

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/> </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** 2.1 </li> <li> **Beispielwert:**<br/> end </li><li> **Beschreibung:**<br/>Das end-Ereignis bedeutet, dass das SDK einen close-Aufruf an das Backend sendet. Bei Empfang dieses Ereignisses schließt das Backend die Sitzung für dieses Video und führt keine weitere Verarbeitung durch. <br/>Wenn das Medium zu 100 % abgeschlossen wurde, sollte dies nach `s:event:type=complete.` gesendet werden. Weitere Informationen finden Sie unter [Inhaltsbeendigung](audio-video-parameters.md#content-complete). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>nicht verfügbar </li> <li> **Heartbeats:**<br/> (s:event:type=end) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Qualitätsmetriken {#quality-metrics}

### Zeit bis Start

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 30.000 </li><li> **Beschreibung:**<br/>Dieser Wert wird standardmäßig auf 0 festgelegt, wenn Sie ihn nicht über das QoSObject einstellen. Sie stellen diesen Wert in Millisekunden ein. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l:stream:startup_time) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Zeit bis Start </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Pufferereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 2 </li><li> **Beschreibung:**<br/>Die Anzahl der Pufferereignisse (Integer). Diese Metrik wird als Anzahl der Pufferereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Pufferereignisse </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Gesamtpufferdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 15 </li><li> **Beschreibung:**<br/>Die insgesamt mit Puffern verbrachte Zeit (Sekunden, Integer). Dieser Wert wird als Summe aller Pufferereignis-Zeitspannen berechnet, die während einer Wiedergabesitzung aufgetreten sind. Der Wert wird im Zeitformat (HH:MM:SS) im Analysis Workspace und in Reports &amp; Analytics angezeigt. In Datenfeeds, Data Warehouse und Reporting APIs werden die Werte in Sekundenschnelle angezeigt. <br/>**Releasedatum: 13.09.2018**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Heartbeat:**<br/> (l:event:duration) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Gesamtpufferdauer </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Bitratenänderungen

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Ereignis </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> „3“ </li><li> **Beschreibung:**<br/>Die Anzahl der Bitratenänderungen. Dieser Wert wird als Summe aller Bitratenänderungs-Ereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Bitratenänderungen </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Fehler

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Die Anzahl der aufgetretenen Fehler (Integer). Dieser Wert wird als Summe aller Fehlerereignisse berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Fehlerereignisse </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Dropped Frames

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 1 </li><li> **Beschreibung:**<br/>Die Anzahl der Dropped Frames (Integer). Dieser Wert wird als Summe aller Dropped Frames berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Dropped Frames </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Drops vor Start

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Gibt an, wie oft ein Benutzer das Video vor dem Start beendet hat. Diese Metrik wird auf 1 gesetzt, wenn kein Inhalt gerendert wurde, unabhängig von Werbeanzeigen.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Drops vor Start </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis gesetzt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Puffer betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der von Pufferung betroffenen Streams. Diese Metrik wird auf 1 gesetzt, wenn mindestens ein Pufferereignis während einer Wiedergabesitzung aufgetreten ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Von Puffer betroffene Streams </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis gesetzt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Bitratenänderung betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams, in denen Bitratenänderungen aufgetreten sind. Diese Metrik wird auf 1 gesetzt, wenn mindestens ein Bitratenänderungs-Ereignis während einer Wiedergabesitzung aufgetreten ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtname:**<br/> Von Bitratenänderung betroffene Streams </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis gesetzt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Durchschnittliche Bitrate

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> 3200 </li><li> **Beschreibung:**<br/>Die durchschnittliche Bitrate (in Kbit/s, Integer). Diese Metrik wird als gewichteter Durchschnitt aller Bitratenwerte im Zusammenhang mit der Wiedergabedauer berechnet, die während einer Wiedergabesitzung aufgetreten sind.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Heartbeat:**<br/> (l:stream:bitrate) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Durchschnittliche Bitrate </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Von Fehlern betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams, in denen ein Fehlerereignis auftrat (daher, `trackError` wurde während der Wiedergabesitzung aufgerufen und ein `type=error`-Aufruf in Heartbeat erstellt). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>error) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Von Fehlern betroffene Streams </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>error) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis gesetzt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Dropped Frames betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** beliebig </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams mit Dropped Frames. Diese Metrik wird auf 1 gesetzt, wenn mindestens ein Dropped Frame während einer Wiedergabesitzung aufgetreten ist.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrames) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Verfügbar:**<br/>ja </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/>Von Dropped Frames betroffene Streams </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>droppedFrames) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis gesetzt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Von Unterbrechung betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** 1.5 (oder höher) </li> <li> **Beispielwert:**<br/> TRUE </li><li> **Beschreibung:**<br/>Die Anzahl der Streams, in denen ein Unterbrechungsereignis auftritt. Diese Metrik wird auf 1 gesetzt, wenn während der Wiedergabe mindestens ein Unterbrechungsereignis aufgetreten ist. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stall) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Wenn dieses Ereignis gesetzt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.

### Unterbrechungsereignisse

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zeichenfolge </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** 1.5 (oder höher) </li> <li> **Beispielwert:**<br/> „3“ </li><li> **Beschreibung:**<br/>Die Anzahl der Wiedergabeunterbrechungen während einer Wiedergabesitzung. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul> |



### Gesamt-Unterbrechungsdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel:**<br/>automatisch festgelegt </li> <li> **API-Schlüssel:**<br/>nicht verfügbar </li> <li> **Erforderlich:**<br/>nein </li> <li> **Typ:**<br/>Zahl </li> <li> **Gesendet mit:**<br/> Media Close </li> <li> **Min. SDK-Version:** 1.5 (oder höher) </li> <li> **Beispielwert:**<br/> 12 </li><li> **Beschreibung:**<br/>Die Gesamtzeit (Sekunden, Integer), für die die Wiedergabe während einer Wiedergabesitzung unterbrochen wurde. Kunden müssen eigene Verarbeitungsregeln erstellen, damit der Wert für Berichte zur Verfügung steht.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Verfügbar:**<br/>Verwenden Sie eine anwenderspezifische Verarbeitungsregel. </li> <li> **Reservierte Variable:**<br/>Ereignis </li> <li> **Berichtsname:**<br/> </li> <li> **Kontextdaten:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Datenfeed:**<br/>nicht verfügbar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> |



## Verwandte APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

