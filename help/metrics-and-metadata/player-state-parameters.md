---
title: Player-Statusparameter
description: In diesem Thema werden Player-Status-Tracking-Parameter beschrieben.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 28%

---


# Player-Statusparameter{#player-state-parameters}

In diesem Thema wird eine Liste der Player-Statusdaten vorgestellt, die Adobe über Lösungsvariablen erfasst.

Beschreibung der Tabellendaten:

* **Implementierung:** Angaben zu den Implementierungswerten und -anforderungen
   * *Schlüssel* - Variable, die entweder manuell in Ihrer App oder automatisch vom Adobe Media SDK festgelegt wird.
   * *Erforderlich* - Gibt an, ob der Parameter für das allgemeine Video-Tracking erforderlich ist.
   * *Typ* - Gibt den Typ der festzulegenden Variablen an, nämlich Zeichenfolge oder Zahl.
   * *Gesendet mit* - Gibt an, wann die Daten gesendet werden: *Media Start* ist der Analytics-Aufruf beim Medienstart, *Ad Start* der Aufruf beim Anzeigenstart usw. *Close* ist der zusammengefasste Analytics-Aufruf, der am Ende der Mediensitzung oder am Ende der Anzeige, des Kapitels usw. vom Heartbeat-Server direkt an den Analytics-Server gesendet wird. Die Aufrufe zum Schließen sind in Netzwerk-Paketaufrufen nicht verfügbar.
   * *Min. SDK-Version* - Gibt an, welche SDK-Version Sie für den Zugriff auf den Parameter benötigen.
   * *Beispielwert* - Bietet ein Beispiel für die Verwendung häufiger Variablen.
* **Netzwerkparameter:** Zeigt die Werte an, die an Adobe Analytics- oder Heartbeat-Server übergeben werden. Diese Spalte enthält die Namen der Parameter, die in den von Adobe Media SDKs generierten Netzwerkaufrufen dargestellt werden.
* **Berichte:** Informationen zur Ansicht und Analyse der Videodaten.
   * *Verfügbar* - Zeigt an, ob die Daten standardmäßig im Reporting verfügbar sind (*Ja*) oder ob eine benutzerdefinierte Einrichtung erforderlich ist (*Benutzerdefiniert*).
   * *Reservierte Variable* - Gibt an, ob die Daten als Ereignis, eVar, prop oder Klassifizierung in einer reservierten Variablen erfasst werden.
   * *Berichtsname* - Name des Adobe Analytics-Berichts für eine Variable
   * *Kontextdaten* - Name der Adobe Analytics-Kontextdaten, die an den Reporting-Server übergeben und in Verarbeitungsregeln verwendet werden.
   * *Daten-Feed* - Spaltenname für eine Variable in Clickstream- oder Live-Stream-Daten-Feeds
   * *Audience Manager* - Trait Name in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändern Sie nicht die Klassifizierungsnamen für Variablen, die unter Berichterstellung/Reservierte Variable als „Klassifizierung“ beschrieben sind.\
>Die Medienklassifizierungen werden definiert, wenn eine Report Suite für das Medien-Tracking aktiviert ist. Adobe fügt von Zeit zu Zeit neue Eigenschaften hinzu. In diesem Fall müssen Kunden ihre Report Suites erneut aktivieren, um Zugriff auf die neuen Medieneigenschaften zu erhalten. Während des Aktualisierungsvorgangs ermittelt Adobe anhand der Namen der Variablen, ob die Klassifizierungen aktiviert sind. Wenn eine fehlt, fügt Adobe die fehlenden erneut hinzu.



## Player-Statuseigenschaften {#player-state-properties}

Die Tabelle mit den Player-Statusverfolgungseigenschaften ist in die folgenden fünf Abschnitte unterteilt:

* Vollbild
   * Von Vollbild betroffene Streams
   * Vollbildanzahl
   * Gesamtdauer im Vollbildmodus
* Beschriftung schließen
   * Von Untertiteln betroffene Streams
   * Anzahl der Untertitel
   * Untertitel - Dauer gesamt
* Stumm
   * Von Mute betroffene Streams
   * Stummzähler
   * Gesamtdauer der Stummschaltung
* Bild in Bild
   * Von Picture in Picture betroffene Streams
   * Picture-in-Picture-Zähler
   * Gesamtdauer des Bilds
* Im Brennpunkt
   * Von InFocus betroffene Streams
   * Fokusanzahl
   * Im Fokus Gesamtdauer

### Vollbildeigenschaften

#### Von Vollbild betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der Streams, die vom Vollbildmodus betroffen sind. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Vollbild betroffene Berichtsnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **Datenfeed **<br/>videostatefullscreen</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.fullscreen.set)</li> </ul> |

#### Vollbildanzahl

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der ein Vollbild angezeigt wurde. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreencount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsname **<br/>Vollbildanzahl</li> <li> **Kontextdaten **<br/>(videostatefullscreencount)<br/> </li> <li> **Datenfeed **<br/>videostatefullscreenCount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatefullscreen-count)</li> </ul> |



#### Gesamtdauer im Vollbildmodus

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Dauer der Anzeige eines Vollbilds. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreen-time)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Dauer des Berichtsnamens **<br/>im Vollbildmodus</li> <li> **Kontextdaten **<br/>(videostatefullscreen-time)<br/> </li> <li> **Datenfeed **<br/>videostatefullscreentime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatefullscreen-time)</li> </ul> |


### Untertiteleigenschaften schließen

#### Von Untertiteln betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der Streams, die von der Untertitel-Funktion betroffen sind. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Untertitelung betroffene Berichtnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.closedcaptioning.set)<br/> </li> <li> **Datenfeed **<br/>videostateclosedcaptionierung</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.closedcaptioning.set)</li> </ul> |


#### Anzahl der Untertitel

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der Untertitel ausgewählt wurden. This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningcount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Anzahl der Untertitel für **<br/>Berichtname</li> <li> **Kontextdaten **<br/>(videostateclosedcaptioningcount)<br/> </li> <li> **Datenfeed **<br/>videostateclosedcaptioningcount</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptioningcount)</li> </ul> |


#### Untertitel - Dauer gesamt

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Zeitdauer der Auswahl von &quot;Untertitel&quot;. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningtime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Dauer der **<br/>Untertitel des Berichts</li> <li> **Kontextdaten **<br/>(videostateclosedcaptioningtime)<br/> </li> <li> **Datenfeed **<br/>videostateclosedcaptiontime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptioningtime)</li> </ul> |


### Stummeigenschaften

#### Von Mute betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der von Mute betroffenen Streams. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Stummschaltung betroffene Berichtsnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.mute.set)<br/> </li> <li> **Datenfeed **<br/>-Videostatusdatei</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.mute.set)</li> </ul> |

#### Stummzähler

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der Mute ausgewählt wurde. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutecount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Name **<br/>der Stummzahl</li> <li> **Kontextdaten **<br/>(videostatemutecount)<br/> </li> <li> **Datenfeed **<br/>videostatemutecount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatemutecount)</li> </ul> |

#### Gesamtdauer der Stummschaltung

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Zeitdauer, für die Mute ausgewählt wurde. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutetime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtname **<br/>- Täuschungsdauer</li> <li> **Kontextdaten **<br/>(videostatemutetime)<br/> </li> <li> **Datenfeed **<br/>videostatemutetime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatemutetime)</li> </ul> |


### Picture in Picture Properties


#### Von Picture in Picture betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der von Picture in Picture betroffenen Streams. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Bild in Bild betroffene Berichtnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.pictureinpicture.set)<br/> </li> <li> **Datenfeed **<br/>videostatepictureinpicture</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.pictureinpicture.set)</li> </ul> |


#### Picture-in-Picture-Zähler

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der Bild in Bild angezeigt wurde. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturecount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Bild des Berichtnamens **<br/>in der Bildanzahl</li> <li> **Kontextdaten **<br/>(videostatepictureinpicturecount)<br/> </li> <li> **Datenfeed **<br/>videostatepictureinpicturecount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatepictureinpicturecount)</li> </ul> |


#### Gesamtdauer des Bilds

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Zeitdauer, in der Bild in Bild angezeigt wurde. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturetime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsnamenbild **<br/>in Bilddauer</li> <li> **Kontextdaten **<br/>(videostatepictureinpicturetime)<br/> </li> <li> **Datenfeed **<br/>videostatepictureinpicturetime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatepictureinpicturetime)</li> </ul> |


### In Fokuseigenschaften

#### Von InFocus betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der von InFocus betroffenen Streams. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von InFocus betroffene Berichtnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.infocus.set)<br/> </li> <li> **Datenfeed **<br/>videostateinfocus</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.infocus.set)</li> </ul> |


#### Fokusanzahl

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der im Fokus angezeigt wurde. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsname **<br/>in Fokuszahl</li> <li> **Kontextdaten **<br/>(videostateinfocuscount)<br/> </li> <li> **Datenfeed **<br/>videostateinfocuscount</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocuscount)</li> </ul> |


#### Im Fokus Gesamtdauer

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Zeitdauer im Fokus wurde angezeigt. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Wichtig** Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsname **<br/>in Fokusdauer</li> <li> **Kontextdaten **<br/>(videostateinfocustime)<br/> </li> <li> **Datenfeed **<br/>videostateinfocustime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocustime)</li> </ul> |



## Verwandte APIs {#related_apis_section}

BENÖTIGT: Hinzufügen API-Links zu Dokumenten:
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* Javascript - [createStateObject](https://need)
