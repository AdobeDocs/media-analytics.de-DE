---
seo-title: Verfolgungsübersicht
title: Verfolgungsübersicht
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Verfolgungsübersicht{#tracking-overview}

>[!IMPORTANT]
>
>Diese Dokumentation behandelt die Verfolgung in Version 2.x des SDK. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen.](/help/sdk-implement/download-sdks.md)

## Player-Ereignisse

Das Tracking der Core-Wiedergabe umfasst die Verfolgung der Medienladung, des Medienstarts, der Medienpause und des Medienabschlusses. Obwohl nicht zwingend erforderlich, sind das Tracking von Puffern und Suchen ebenfalls Kernkomponenten für die Verfolgung der Inhaltswiedergabe. Identifizieren Sie in Ihrer Medienplayer-API die Player-Ereignisse, die mit den Tracking-Aufrufen des Medien-SDK übereinstimmen, und kodieren Sie Ihre Ereignishandler, um Tracking-APIs aufzurufen und erforderliche und optionale Variablen zu füllen.

### Beim Laden der Medien

* Erstellen Sie das Medienobjekt.
* Metadaten ausfüllen
* Aufruf `trackSessionStart`;Beispiel: `trackSessionStart(mediaObject, contextData)`

### Beim Medienstart

* Aufruf    `trackPlay`

### Bei Pause/Fortsetzung

* Aufruf    `trackPause`
* Call `trackPlay`   _when playback resumes_

### Bei Medienende

* Aufruf    `trackComplete`

### Bei Medienabbruch

* Aufruf    `trackSessionEnd`

### Wenn das Scrubbing beginnt

* Aufruf    `trackEvent(SeekStart)`

### Wenn das Scrubbing endet

* Aufruf    `trackEvent(SeekComplete)`

### Wenn die Pufferung beginnt

* Aufruf    `trackEvent(BufferStart);`

### Wenn die Pufferung endet

* Aufruf    `trackEvent(BufferComplete);`

>[!TIP]
>
>Die Position der Abspielleiste wird als Teil des Einrichtungs- und Konfigurationscodes festgelegt. Weitere Informationen `getCurrentPlayheadTime`finden Sie unter [Übersicht: Allgemeine Umsetzungsleitlinien.](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## Implementierung {#implement}

1. **Tracking-Ersteinrichtung:** Ermitteln Sie, wann der Anwender die Wiedergabe auslöst (wenn er die Play-Schaltfläche betätigt und/oder die automatische Wiedergabe aktiviert ist), und erstellen Sie eine `MediaObject`-Instanz mithilfe der folgenden Medieninformationen: Inhaltsname, Inhalts-ID, Inhaltsdauer und Streamtyp.

   **`MediaObject`Referenz:**

   | Variablenname | Beschreibung | erforderlich |
   |---|---|---|
   | `name` | Inhaltsname | Ja |
   | `mediaid` | Eindeutige Inhaltskennung | Ja |
   | `length` | Inhaltsdauer | Ja |
   | `streamType` | Streamtyp | Ja |
   | `mediaType` | Medientyp (Audio- oder Videoinhalt) | Ja |

   **`StreamType`Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `VOD` | Streamtyp für Video on Demand |
   | `LIVE` | Streamtyp für Live-Inhalt |
   | `LINEAR` | Streamtyp für Linear-Inhalt |
   | `AOD` | Streamtyp für Audio on Demand |
   | `AUDIOBOOK` | Streamtyp für Hörbuch |
   | `PODCAST` | Streamtyp für Podcast |

   **`MediaType`Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `Audio` | Medientyp für Audiostreams. |
   | `Video` | Medientyp für Videostreams. |

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Metadaten anhängen:** Optional können standardmäßige und/oder anwenderdefinierte Metadatenobjekte über Kontextdatenvariablen an die Tracking-Sitzung angehängt werden.

   * **Standardmetadaten:**

      >[!NOTE]
      >
      >Das Anhängen des Standard-Metadatenobjekts an das Medienobjekt ist optional.

      Instanziieren Sie ein Standard-Metadatenobjekt, füllen Sie die gewünschten Variablen aus und setzen Sie das Metadatenobjekt auf das Media Heartbeat-Objekt.

      Sehen Sie hier die umfassende Liste der verfügbaren-Metadaten: [Audio- und Videoparameter.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Anwenderdefinierte Metadaten:** Erstellen Sie ein Variablenobjekt für die anwenderspezifischen Variablen und fügen Sie die Daten für diesen Inhalt ein.

1. **Verfolgen Sie die Absicht, die Wiedergabe zu starten:** Um mit dem Tracking einer Sitzung zu beginnen, rufen Sie `trackSessionStart` in der Heartbeat-Instanz auf.

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Daten/Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Tatsächlichen Wiedergabebeginn verfolgen:** Identifizieren Sie das Ereignis für den Anfang der Wiedergabe im Medienplayer, sobald der erste Frame des Inhalts auf dem Bildschirm angezeigt wird, und rufen Sie `trackPlay` auf.

1. **Tracking des Wiedergabeendes:** Identifizieren Sie das Ereignis für den Abschluss der Wiedergabe im Medienplayer, wenn der Inhalt bis zum Ende angesehen wurde, und rufen Sie `trackComplete` auf.

1. **Tracking des Sitzungsendes:** Identifizieren Sie das Ereignis beim Entladen/Schließen der Wiedergabe im Medienplayer, wenn der Anwender den Inhalt schließt und/oder der Inhalt abgeschlossen ist und entladen wird, und rufen Sie `trackSessionEnd` auf.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markiert das Ende einer Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Tracking aller möglichen Pausenszenarien:** Identifizieren Sie das Ereignis aus dem Medienplayer, das das Anhalten verursacht, und rufen Sie `trackPause` auf.

   **Pausenszenarios:** Identifizieren Sie alle Szenarios, in denen der Player angehalten wird, und stellen Sie sicher, dass `trackPause` ordnungsgemäß aufgerufen wird. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Anwender betätigt in der App die Pause-Schaltfläche.
   * Der Player geht selbstständig in den Pausenstatus über.
   * (*Mobile Apps*): Der Anwender setzt die App in den Hintergrund, Sie möchten die Sitzung jedoch geöffnet halten.
   * (*Mobile Apps*): Es tritt eine Systemunterbrechung auf, die dafür sorgt, dass die Anwendung im Hintergrund ausgeführt wird. Wenn der Anwender beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Anwender den Inhalt fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei Wiedergabe und/oder Fortsetzen nach Pause und rufen Sie `trackPlay` auf.

   >[!TIP]
   >
   >Dies kann dieselbe Ereignisquelle sein, die in Schritt 4 verwendet wurde. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. Suchen Sie nach den Wiedergabesuchereignissen vom Medienplayer. Wenn Sie die Benachrichtigung zum Suchstartereignis erhalten, verfolgen Sie die Suche mit dem `SeekStart`-Ereignis.
1. Wenn Sie die Benachrichtigung zum Suchabschluss vom Medienplayer erhalten, zeichnen Sie das Suchende mit dem `SeekComplete`-Ereignis auf.
1. Suchen Sie nach den Wiedergabepufferereignissen aus dem Medienplayer. Wenn Sie die Benachrichtigung zum Pufferstartereignis erhalten, verfolgen Sie die Pufferung mit dem `BufferStart`-Ereignis.
1. Wenn Sie die Benachrichtigung zum Pufferabschluss vom Medienplayer erhalten, verfolgen Sie das Ende der Pufferung mit dem `BufferComplete`-Ereignis.

In den folgenden plattformspezifischen Themen finden Sie Beispiele für jeden Schritt und die in Ihren SDKs enthaltenen Beispielplayer.

Ein einfaches Beispiel für das Playback-Tracking finden Sie unter dieser Verwendung mit dem JavaScript 2.x-SDK auf einem HTML5-Player:

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
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## Überprüfen {#validate}

Informationen zur Validierung Ihrer Implementierung finden Sie unter [Validierung.](/help/sdk-implement/validation/validation-overview.md)

