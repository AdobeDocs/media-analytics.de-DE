---
title: Tracking-Inhaltswiedergabe – Erklärung
description: 'Erfahren Sie mehr über das Tracking der Core-Wiedergabe, einschließlich des Trackings der Medienladung, des Medienstarts, der Medienpause und des Medienabschlusses. '
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 97%

---

# Tracking-Übersicht{#tracking-overview}

Diese Dokumentation behandelt das Tracking in der Version 2.x des SDK.

>[!IMPORTANT]
>
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/getting-started/download-sdks.md)

## Player-Ereignisse

Das Tracking der Core-Wiedergabe beinhaltet das Tracking des Ladens des Mediums, den Medienstart, die Medienpause und den Medienabschluss. Obwohl dies nicht obligatorisch ist, sind die Tracking-Pufferung und -Suche auch Kernkomponenten, die zum Tracking der Inhaltswiedergabe verwendet werden. Identifizieren Sie in Ihrer Medienplayer-API die Player-Ereignisse, die den Media SDK-Tracking-Aufrufen entsprechen, und codieren Sie Ihre Ereignis-Handler, um Tracking-APIs aufzurufen und erforderliche und optionale Variablen zu füllen.

### Beim Laden der Medien

* Medienobjekt erstellen
* Metadaten befüllen
* Aufruf `trackSessionStart`. Beispiel: `trackSessionStart(mediaObject, contextData)`

### Beim Medienstart

* Aufruf `trackPlay`

### Bei Pause/Fortsetzung

* Aufruf `trackPause`
* Aufruf `trackPlay`   _, wenn die Wiedergabe fortgesetzt wird_

### Bei Medienende

* Aufruf `trackComplete`

### Bei Medienabbruch

* Aufruf `trackSessionEnd`

### Wenn das Scrubbing beginnt

* Aufruf `trackEvent(SeekStart)`

### Wenn das Scrubbing endet

* `trackEvent(SeekComplete)`
Änderungen verwerfen

### Wenn die Pufferung beginnt

* Aufruf `trackEvent(BufferStart);`

### Wenn die Pufferung endet

* Aufruf `trackEvent(BufferComplete);`


## Implementierung {#implement}

1. **Tracking-Ersteinrichtung:** Ermitteln Sie, wann der Anwender die Wiedergabe auslöst (wenn er die Play-Schaltfläche betätigt und/oder die automatische Wiedergabe aktiviert ist), und erstellen Sie eine `MediaObject`-Instanz mithilfe der folgenden Medieninformationen: Inhaltsname, Inhalts-ID, Inhaltsdauer und Streamtyp.

   **`MediaObject`-Referenz:**

   | Variablenname | Beschreibung | erforderlich |
   |---|---|---|
   | `name` | Inhaltsname | Ja |
   | `mediaid` | Eindeutige Kennung des Inhalts | Ja |
   | `length` | Länge des Inhalts | Ja |
   | `streamType` | Stream-Typ | Ja |
   | `mediaType` | Medientyp (Audio- oder Videoinhalt) | Ja |

   **`StreamType`-Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `VOD` | Streamtyp für Video on Demand |
   | `LIVE` | Streamtyp für Live-Inhalt |
   | `LINEAR` | Streamtyp für Linear-Inhalt |
   | `AOD` | Streamtyp für Audio on Demand |
   | `AUDIOBOOK` | Streamtyp für Hörbuch |
   | `PODCAST` | Streamtyp für Podcast |

   **`MediaType`-Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `Audio` | Medientyp für Audiostreams. |
   | `Video` | Medientyp für Videostreams. |

   Das allgemeine Format für die Erstellung von `MediaObject` ist `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Metadaten anhängen -** Optional können Standard- bzw. benutzerdefinierte Metadatenobjekte über Kontextdatenvariablen an die Tracking-Sitzung angehängt werden.

   * **Standard-Metadaten -**

     >[!NOTE]
     >
     >Das Anhängen des Standard-Metadatenobjekts an das Medienobjekt ist optional.

     Instanziieren Sie ein Standard-Metadatenobjekt, füllen Sie die gewünschten Variablen aus und setzen Sie das Metadatenobjekt auf das Media Heartbeat-Objekt.

     Sehen Sie hier die umfassende Liste der verfügbaren-Metadaten: [Audio- und Videoparameter.](../../implementation/variables/audio-video-parameters.md)

   * **Anwenderdefinierte Metadaten:** Erstellen Sie ein Variablenobjekt für die anwenderspezifischen Variablen und fügen Sie die Daten für diesen Inhalt ein.

1. **Verfolgen Sie die Absicht, die Wiedergabe zu starten:** Um mit dem Tracking einer Sitzung zu beginnen, rufen Sie `trackSessionStart` in der Heartbeat-Instanz auf.

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Daten/Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >Wenn Sie keine benutzerdefinierten Metadaten verwenden, senden Sie einfach ein leeres Objekt für das `data`-Argument in `trackSessionStart`.

1. **Tatsächlichen Wiedergabebeginn verfolgen:** Identifizieren Sie das Ereignis für den Anfang der Wiedergabe im Medienplayer, sobald der erste Frame des Inhalts auf dem Bildschirm angezeigt wird, und rufen Sie `trackPlay` auf.

1. **Tracking des Wiedergabeendes:** Identifizieren Sie das Ereignis für den Abschluss der Wiedergabe im Medienplayer, wenn der Inhalt bis zum Ende angesehen wurde, und rufen Sie `trackComplete` auf.

1. **Tracking des Sitzungsendes:** Identifizieren Sie das Ereignis beim Entladen/Schließen der Wiedergabe im Medienplayer, wenn der Anwender den Inhalt schließt und/oder der Inhalt abgeschlossen ist und entladen wird, und rufen Sie `trackSessionEnd` auf.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markiert das Ende einer Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Jeder andere `track*`-API-Aufruf nach `trackSessionEnd` wird ignoriert, mit Ausnahme von `trackSessionStart` für eine neue Tracking-Sitzung.

1. **Tracking aller möglichen Pausenszenarien:** Identifizieren Sie das Ereignis aus dem Medienplayer, das das Anhalten verursacht, und rufen Sie `trackPause` auf.

   **Pausenszenarios:** Identifizieren Sie alle Szenarios, in denen der Player angehalten wird, und stellen Sie sicher, dass `trackPause` ordnungsgemäß aufgerufen wird. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Benutzer drückt in der App die Pausetaste.
   * Die Wiedergabe wird vom Player selbst pausiert.
   * (*Mobile Apps*) - Der Benutzer bewegt die App in den Hintergrund, aber Sie möchten, dass die Sitzung der App geöffnet bleibt.
   * (*Mobile Apps*) - Eine beliebige Systemunterbrechung tritt ein, die dazu führt, dass eine App im Hintergrund ausgeführt wird. Beispielsweise erhält der Benutzer einen Anruf oder ein Pop-up aus einer anderen App, aber Sie möchten, dass die App-Sitzung fortgeführt wird, damit der Benutzer den Inhalt ab dem Zeitpunkt der Unterbrechung wieder fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei Wiedergabe und/oder Fortsetzen nach Pause und rufen Sie `trackPlay` auf.

   >[!TIP]
   >
   >Diese Ereignisquelle kann mit der in Schritt 4 verwendeten identisch sein. Stellen Sie sicher, dass jeder `trackPause()`API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Wiedergabe fortgesetzt wird.

1. Suchen Sie nach den Wiedergabesuchereignissen vom Medienplayer. Wenn Sie die Benachrichtigung zum Suchstartereignis erhalten, verfolgen Sie die Suche mit dem `SeekStart`-Ereignis.
1. Wenn Sie die Benachrichtigung zum Suchabschluss vom Medienplayer erhalten, zeichnen Sie das Suchende mit dem `SeekComplete`-Ereignis auf.
1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis.
1. Wenn Sie die Benachrichtigung zum Pufferabschluss vom Medienplayer erhalten, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Ereignis.

In den folgenden plattformspezifischen Themen finden Sie Beispiele für jeden Schritt. Außerdem enthalten Ihre SDKs Beispiel-Player.

Ein einfaches Beispiel für das Wiedergabe-Tracking finden Sie in der Verwendung des JavaScript 2.x SDK in einem HTML5-Player:

```js
/* Call on media start */
if (e.type == "play") {

    // Check for start of media
    if (!sessionStarted) {
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>,
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/
        var mediaInfo = MediaHeartbeat.createMediaObject(
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration,
          MediaHeartbeat.StreamType.VOD);

        /* Set custom context data */
        var customVideoMetadata = {
            isUserLoggedIn: "false",
            tvStation: "Sample TV station",
            programmer: "Sample programmer"
        };

        /* Set standard video metadata */     
        var standardVideoMetadata = {};
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     

        // Start Session
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    

        // Track play
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     

    } else {
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    }
};

/* Call on video complete */
if (e.type == "ended") {
    console.log("video ended");
    this.mediaHeartbeat.trackComplete();
    this.mediaHeartbeat.trackSessionEnd();
    sessionStarted = false;     
};

/* Call on pause */
if (e.type == "pause") {
    this.mediaHeartbeat.trackPause();
};

/* Call on scrub start */
if (e.type == "seeking") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};

/* Call on scrub stop */
if (e.type == "seeked") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};

/* Call on buffer start */
if (e.type == "buffering") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == "buffered") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## Überprüfen {#validate}

Informationen zur Validierung Ihrer *alten* Implementierung finden Sie unter [Legacy-Validierung](/help/legacy/validation/validation-overview.md).
