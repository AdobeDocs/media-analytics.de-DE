---
title: Player-Statusparameter
description: In diesem Thema werden Player-Status-Tracking-Parameter beschrieben.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '2236'
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

Die Player-Statusverfolgungsfunktionen können an einen Audio- oder Videostream angehängt werden. Standardisierte Player-Statusverfolgungsmetriken werden als Lösungsvariablen gespeichert. Die Standardzustände sind: fullScreen, mute, closeCaption, pictureInPicture und inFocus.

### Vollbildeigenschaften

#### Vom Vollbildmodus betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der Streams, die vom Vollbildmodus betroffen sind. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Vollbild betroffene Berichtsnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **Datenfeed **<br/>media.states.fullscreen</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.fullscreen.set)</li> </ul> |

#### Anzahl der Vollbildmodi

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der ein Vollbild angezeigt wurde. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Wichtig **<br/>Wenn dieses Ereignis eingestellt ist, entspricht die Anzahl der Videowiedergaben der Anzahl der Videowiedergaben im Vollbildmodus. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.count)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsname **<br/>Vollbildanzahl</li> <li> **Kontextdaten **<br/>(media.states.fullscreen.count)<br/> </li> <li> **Datenfeed **<br/>media.stats.fullscreen.count</li> <li> **Audience Manager **<br/>(c_contextData.media.states.fullscreen.count)</li> </ul> |



#### Gesamtdauer der Vollbildmodi

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Dauer der Anzeige eines Vollbilds. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Wichtig **<br/>Wenn dieses Ereignis eingestellt ist, ist die Zeit gleich der Länge des Videos im Vollbildmodus. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.time)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Gesamtdauer des **<br/>Berichts im Vollbildmodus</li> <li> **Kontextdaten **<br/>(media.states.fullscreen.time)<br/> </li> <li> **Datenfeed **<br/>media.states.fullscreen.time</li> <li> **Audience Manager **<br/>(c_contextData.media.states.fullscreen.time)</li> </ul> |


### Untertiteleigenschaften schließen

#### Von verdeckten Untertiteln betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der Streams, die von der Untertitel-Funktion betroffen sind. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Untertitelung betroffene Berichtnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.closedcaptioning.set)<br/> </li> <li> **Datenfeed **<br/>media.states.closeDcaptioning</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.closedcaptioning.set)</li> </ul> |


#### Anzahl der verdeckten Untertitel

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der Untertitel angezeigt wurden. This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **Wichtig **<br/>Wenn dieses Ereignis eingestellt ist, entspricht die Anzahl der Videowiedergaben dem Status &quot;Untertitel&quot;. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(C19)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Anzahl der Untertitel für **<br/>Berichtname</li> <li> **Kontextdaten **<br/>(media.states.closedcaptioning.count)<br/> </li> <li> **Datenfeed **<br/>media.states.closedcaptioning.count</li> <li> **Audience Manager **<br/>(c_contextData.media.states.closedcaptioning.count)</li> </ul> |


#### Gesamtdauer der verdeckten Untertitel

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Dauer der Anzeige von Untertiteln. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Wichtig **<br/>Wenn dieses Ereignis eingestellt ist, ist die Zeit gleich der Dauer des Videos im Status &quot;Untertitel&quot;. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.closedcaptioning.time)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtname **<br/>- Untertitel - Gesamtdauer</li> <li> **Kontextdaten **<br/>(media.states.closedcaptioning.time)<br/> </li> <li> **Datenfeed **<br/>media.states.closedcaptioning.time</li> <li> **Audience Manager **<br/>(c_contextData.media.states.closedcaptioning.time)</li> </ul> |


### Stummeigenschaften

#### Von der Stummschaltung betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der von Mute betroffenen Streams. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Stummschaltung betroffene Berichtsnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.mute.set)<br/> </li> <li> **Datenfeed **<br/>media.states.mute</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.mute.set)</li> </ul> |

#### Anzahl der Stummschaltungen

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der Mute angezeigt wurde. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Wichtig **<br/>Wenn dieses Ereignis eingestellt ist, entspricht die Anzahl der Mute-Status des Videos. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.count)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Name **<br/>der Stummzahl</li> <li> **Kontextdaten **<br/>(media.states.mute.count)<br/> </li> <li> **Datenfeed **<br/>media.states.mute.count</li> <li> **Audience Manager **<br/>(c_contextData.media.states.mute.count)</li> </ul> |

#### Gesamtdauer der Stummschaltungen

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Zeitdauer, in der Mute angezeigt wurde. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Wichtig **<br/>Wenn dieses Ereignis eingestellt ist, ist die Zeit gleich der Länge des Videos im Status &quot;Stumm&quot;. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.time)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsname **<br/>Gesamtdauer der Ton</li> <li> **Kontextdaten **<br/>(media.states.mute.time)<br/> </li> <li> **Datenfeed **<br/>media.states.mute.time</li> <li> **Audience Manager **<br/>(c_contextData.media.states.mute.time)</li> </ul> |


### Picture in Picture Properties


#### Von Picture in Picture betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der von Picture in Picture betroffenen Streams. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von Bild in Bild betroffene Berichtnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.pictureinpicture.set)<br/> </li> <li> **Datenfeed **<br/>media.stats.pictureinpicture</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.pictureinpicture.set)</li> </ul> |


#### Picture-in-Picture-Zähler

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der Bild in Bild angezeigt wurde. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, entspricht die Anzahl der Videoaufnahmen der Anzahl der Aufnahmen im Status &quot;Bild in Bild&quot;. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.count)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Bild des Berichtnamens **<br/>in der Bildanzahl</li> <li> **Kontextdaten **<br/>(media.states.pictureinpicture.count)<br/> </li> <li> **Datenfeed **<br/>media.stats.pictureinpicture.count</li> <li> **Audience Manager **<br/>(c_contextData.media.states.pictureinpicture.count)</li> </ul> |


#### Gesamtdauer des Bilds

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Zeitdauer, in der Bild in Bild angezeigt wurde. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, ist die Zeit gleich der Länge des Videos im Status &quot;Bild im Bild&quot;. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet..   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.time)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsnamenbild **<br/>in Gesamtbilddauer</li> <li> **Kontextdaten **<br/>(media.states.pictureinpicture.time)<br/> </li> <li> **Datenfeed **<br/>media.states.pictureinpicture.time</li> <li> **Audience Manager **<br/>(c_contextData.media.states.pictureinpicture.time)</li> </ul> |


### In Fokuseigenschaften

#### Vom Fokusmodus betroffene Streams

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Anzahl der von InFocus betroffenen Streams. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, ist der einzig mögliche Wert TRUE. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Von InFocus betroffene Berichtnamenstreams **<br/></li> <li> **Kontextdaten **<br/>(a.media.states.infocus.set)<br/> </li> <li> **Datenfeed **<br/>media.states.infocus</li> <li> **Audience Manager **<br/>(c_contextData.a.media.states.infocus.set)</li> </ul> |


#### Anzahl der Fokusmodi

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Häufigkeit, mit der im Fokus angezeigt wurde. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Wichtig **<br/>Wenn dieses Ereignis eingestellt ist, entspricht die Anzahl der Anzahl der Fälle, in denen sich das Video im Fokus befindet. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.count)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsname **<br/>in Fokuszahl</li> <li> **Kontextdaten **<br/>(media.states.infocus.count)<br/> </li> <li> **Datenfeed **<br/>media.states.infocus.count</li> <li> **Audience Manager **<br/>(c_contextData.media.states.infocus.count)</li> </ul> |


#### Gesamtdauer der Fokusmodi

|   Implementierung   | Netzwerkparameter | Berichterstellung |
| --- | --- | --- |
| <ul> <li> **SDK-Schlüssel **<br/>automatisch eingestellt</li> <li> **API-Schlüssel **<br/>- K/A</li> <li> **Erforderliche **<br/>Nr.</li> <li> **Typ **<br/>Nummer</li> <li> **Mit **<br/>Medienabschluss gesendet</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Beispielwert **<br/>TRUE</li><li> ****<br/>BeschreibungDie Zeitdauer im Fokus wurde angezeigt. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Wichtig** <br/> Wenn dieses Ereignis eingestellt ist, ist die Zeit gleich der Länge des Videos im Fokuszustand. Wenn das Ereignis nicht festgelegt wurde, wird kein Wert gesendet.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.time)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Verfügbar **<br/>Ja</li> <li> **Ereignis für reservierte Variablen **<br/></li> <li> **Berichtsname **<br/>in Fokusdauer insgesamt</li> <li> **Kontextdaten **<br/>(media.states.infocus.time)<br/> </li> <li> **Datenfeed **<br/>media.states.infocus.time</li> <li> **Audience Manager **<br/>(c_contextData.media.states.infocus.time)</li> </ul> |

## Eigenschaften-Liste für XDM-Identitäten

In Analytics gespeicherte Daten können für jeden Zweck verwendet werden. Die Player-Statusmetriken können mithilfe von XDM in Adobe Experience Platform importiert und mit Customer Journey Analytics verwendet werden.

| Player-Statuseigenschaft | Zuordnen |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## Verwandte APIs {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
