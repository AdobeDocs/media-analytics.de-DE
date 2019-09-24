---
seo-title: Tracking von Core-Wiedergaben auf Roku
title: Tracking von Core-Wiedergaben auf Roku
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracking von Core-Wiedergaben auf Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Diese Dokumentation behandelt die Verfolgung in Version 2.x des SDK. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](/help/sdk-implement/download-sdks.md)

1. **Einrichtung der anfänglichen Verfolgung**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`Referenz:**

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Videoname | Ja |
   | `mediaid` | Eindeutige ID des Videos | Ja |
   | `length` | Videolänge | Ja |
   | `streamType` | Stream-Typ (siehe _StreamType-Konstanten_ unten) | Ja |
   | `mediaType` | Medientyp (siehe _MediaType-Konstanten_ unten) | Ja |

   **`StreamType`Konstanten:**

   | Konstantenname | Beschreibung   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Streamtyp für Video on Demand |
   | `MEDIA_STREAM_TYPE_LIVE` | Streamtyp für Live-Inhalt |
   | `MEDIA_STREAM_TYPE_LINEAR` | Streamtyp für Linear-Inhalt |
   | `MEDIA_STREAM_TYPE_AOD` | Streamtyp für Audio on Demand |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Streamtyp für Hörbuch |
   | `MEDIA_STREAM_TYPE_PODCAST` | Streamtyp für Podcast |

   **`MediaType`Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Medientyp für Audiostreams. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Medientyp für Videostreams. |

   **Medieninfo-Objekt für Video mit VOD-Inhalt erstellen:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   oder

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Erstellen Sie ein Medieninfo-Objekt für Videos mit AOD-Inhalt:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   oder

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Anhängen von Metadaten**

   Fügen Sie der Verfolgungssitzung optional Standard- und/oder benutzerdefinierte Metadatenobjekte über Kontextdatenvariablen hinzu.

   * **Standard-Metadaten**

      [Standard-Metadaten in JavaScript implementieren](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Das Anhängen des Standard-Metadatenobjekts an das Medienobjekt ist optional.

      * Medien-Metadatenschlüssel API-Referenz: [Standard-Metadatenschlüssel - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und füllen Sie die Daten für dieses Medium aus. Beispiel:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Verfolgung der Absicht, die Wiedergabe zu starten**

   Um mit der Verfolgung einer Mediensitzung zu beginnen, rufen Sie `trackSessionStart` die Media Heartbeat-Instanz auf:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Der zweite Wert ist der benutzerdefinierte Medienmetadatenobjektname, den Sie in Schritt 2 erstellt haben.

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Daten/Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Den tatsächlichen Start der Wiedergabe verfolgen**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Verfolgen Sie den Abschluss der Wiedergabe.**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Ende der Sitzung verfolgen**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >A `trackSessionEnd` marks the end of a tracking session. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.  Tracking-Methode für die Medienwiedergabe, bei der das Laden der Medien und das Aktivieren der aktuellen Sitzung verfolgt wird:

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **Anhängen von Videometadaten**

   Fügen Sie der Videoverfolgungssitzung optional Standard- und/oder benutzerdefinierte Videometadatenobjekte über Kontextdatenvariablen hinzu.

   * **Standard-Videometadaten**

      [Standard-Metadaten in Roku implementieren](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Das Anhängen des Videometadatenobjekts an das Medienobjekt ist optional.

   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und füllen Sie die Daten für dieses Video aus. Beispiel:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Verfolgung der Absicht, die Wiedergabe zu starten**

   Um mit der Verfolgung einer Mediensitzung zu beginnen, rufen Sie `trackSessionStart` die Media Heartbeat-Instanz auf:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >Der zweite Wert ist der benutzerdefinierte Videometadatenobjektname, den Sie in Schritt 2 erstellt haben.

   >[!IMPORTANT]
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Videodaten/-Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Den tatsächlichen Start der Wiedergabe verfolgen**

   Identifizieren Sie das Ereignis für den Anfang der Videowiedergabe im Videoplayer (wenn das erste Videobild auf dem Bildschirm angezeigt wird) und rufen Sie `trackPlay` () auf:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Verfolgen Sie den Abschluss der Wiedergabe.**

   Identifizieren Sie das Ereignis für den Abschluss der Videowiedergabe im Videoplayer (wenn der Inhalt bis zum Ende angesehen wurde) und rufen Sie `trackComplete` () auf:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Ende der Sitzung verfolgen**

   Identifizieren Sie das Ereignis für das Entfernen/Schließen der Videowiedergabe im Videoplayer (wenn der Benutzer das Video schließt und/oder das Video abgeschlossen ist und aus dem Player entfernt wird) und rufen Sie `trackSessionEnd` () auf:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` markiert das Ende einer Videoverfolgungssitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Alle möglichen Pausenszenarien verfolgen**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Szenarios anhalten**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Anwender betätigt in der App die Pause-Schaltfläche.
   * Der Player geht selbstständig in den Pausenstatus über.
   * (*Mobile Apps*): Der Anwender setzt die App in den Hintergrund, Sie möchten die Sitzung jedoch geöffnet halten.
   * (*Mobile Apps*): Es tritt eine Systemunterbrechung auf, die dafür sorgt, dass die Anwendung im Hintergrund ausgeführt wird. Wenn der Benutzer beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Benutzer das Video fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei wiedergegebenen und/oder nach einer Pause wiederaufgenommenen Videos und rufen Sie `trackPlay` auf:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Dies kann dieselbe Ereignisquelle sein, die in Schritt 4 verwendet wurde. Stellen Sie sicher, dass jeder `trackPause()`-API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Videowiedergabe wiederaufgenommen wird.

* Tracking-Szenarios: [VOD-Wiedergabe ohne Werbung](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Der im Roku-SDK enthaltene Beispiel-Player zeigt ein komplettes Tracking-Beispiel.

