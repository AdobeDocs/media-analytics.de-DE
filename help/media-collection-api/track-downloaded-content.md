---
seo-title: Tracking heruntergeladener Inhalte
title: Tracking heruntergeladener Inhalte
uuid: 7186689 d -9602-4 e 3 f -833 c -8297 aae 1 d 009
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracking heruntergeladener Inhalte{#track-downloaded-content}

## Überblick {#section_hcy_3pk_cfb}

Die Downloaded Content API bietet die Möglichkeit, die Mediennutzung zu verfolgen, während ein Anwender offline ist. Beispielsweise lädt ein Anwender eine App herunter und installiert sie auf einem Mobilgerät. Der Anwender lädt dann mit der App Inhalte in den lokalen Speicher auf dem Gerät herunter. Um das Tracking dieser heruntergeladenen Daten zu ermöglichen, hat Adobe die Downloaded Content API entwickelt. Mit dieser API werden Tracking-Daten unabhängig von der Konnektivität des Geräts gespeichert, wenn der Anwender Inhalte aus dem Speicher des Geräts wiedergibt. Wenn der Benutzer die Wiedergabesitzung beendet und das Gerät online ist, werden die gespeicherten Verfolgungsinformationen an die Mediensammlung-API innerhalb einer einzelnen Payload gesendet. Von dort aus erfolgt die Verarbeitung und das Reporting wie gewohnt in der Mediensammlungs-API, auf der diese API basiert.

Vergleichen Sie die beiden Ansätze:

* Mediensammlungs-API

   Mit diesem Echtzeitansatz sendet der Medienplayer Verfolgungsdaten bei jedem Player-Ereignis und sendet alle zehn Sekunden Netzwerkpings (alle eine Sekunde für Anzeigen), eine um eins bis ein Backend.

* Downloaded Content API

   Bei diesem Batch-Verarbeitungsansatz müssen dieselben Sitzungsereignisse erstellt, aber auf dem Gerät gespeichert werden, bis sie als einzelne Sitzung an das Back-End gesendet werden (siehe Beispiel unten).

Jeder Ansatz hat seine Vor- und Nachteile: Die Mediensammlungs-API verfolgt in Echtzeit, aber dies erfordert eine Verbindungsprüfung vor jedem Netzwerkaufruf. Die Downloaded Content API erfordert nur eine Überprüfung der Netzwerkverbindung, hat aber auch einen größeren Speicherbedarf auf dem Gerät.

## Implementierung {#section_jhp_jpk_cfb}

### Ereignisschemata

Die heruntergeladene Inhalts-API basiert auf der Mediensammlungs-API. Die Ereignisdaten, die von Ihren Player-Batches und -senden gesendet werden, müssen daher dieselben Ereignisschemas wie in der Media Collection API verwenden. For information on these schemas, see: [Overview;](/help/media-collection-api/mc-api-overview.md) and [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Reihenfolge der Ereignisse

* Das erste Ereignis in der Batch-Payload muss `sessionStart` sein.
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. Wenn dieser Parameter nicht vorhanden ist oder auf false gesetzt ist, antwortet die Downloaded Content API mit dem Antwortcode 400 (Anfragefehler). Dies ist der Fall, wenn das Back-End zwischen heruntergeladenen und Live-Inhalten unterscheiden und sie entsprechend verarbeiten kann. (Beachten Sie: wenn `media.downloaded: true` auf eine Live-Sitzung eingestellt ist, wird dies ebenfalls zu einer Antwort mit dem Code 400 aus der Mediensammlungs-API führen)

* Es liegt an einer korrekten Implementierung, Abspielereignisse in der Reihenfolge ihres Auftretens richtig zu speichern.

### Antwortcodes

* 201 - Created: Successful Request; die Daten sind gültig und die Sitzung wurde erstellt und wird verarbeitet.
* 400 - Bad Request; die Schemavalidierung ist fehlgeschlagen, alle Daten werden verworfen, es werden keine Sitzungsdaten verarbeitet.

## Integration mit Adobe Analtyics {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. Dies sind Zeitstempel für die ersten und letzten empfangenen Ereignisse (Start und Beendigung). Mit diesem Mechanismus kann eine abgeschlossene Mediensitzung am richtigen Zeitpunkt platziert werden (d. h., auch wenn der Benutzer mehrere Tage nicht online ist, wird die Mediensitzung zu dem Zeitpunkt aufgezeichnet, zu dem der Inhalt tatsächlich angezeigt wurde). Sie müssen dieses Verfahren auf der Seite von Adobe Analytics aktivieren, indem Sie einen *optionalen Zeitstempel für die Report Suite erstellen*. Informationen zum Aktivieren eines optionalen Zeitstempel für die Report Suite finden Sie unter [Optionale Zeitstempel.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## Vergleich von Beispielsitzungen {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### Mediensammlungs-API

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### Downloaded Content API

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

