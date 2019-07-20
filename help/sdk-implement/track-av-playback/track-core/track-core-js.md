---
seo-title: Tracking von Core-Wiedergaben auf JavaScript
title: Tracking von Core-Wiedergaben auf JavaScript
uuid: 3 d 6 e 0 ab 1-899 a -43 c 3-b 632-8276 e 84345 ab
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Tracking von Core-Wiedergaben auf JavaScript{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Diese Dokumentation enthält die Verfolgung in Version 2. x des SDK. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](../../../sdk-implement/download-sdks.md)

1. **Initiales Tracking-Setup**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Medienname | Ja |
   | `mediaid` | Eindeutige Medienkennung | Ja |
   | `length` | Medienlänge | Ja |
   | `streamType` | Stream type (see _StreamType constants_ below) | Ja |
   | `mediaType` | Media type (see _MediaType constants_ below) | Ja |

   **`StreamType`Konstanten:**

   | Konstantenname | Beschreibung   |
   |---|---|
   | `VOD` | Streamtyp für Video on Demand |
   | `LIVE` | Streamtyp für Live-Inhalt |
   | `LINEAR` | Streamtyp für Linear-Inhalt |
   | `AOD` | Stream-Typ für Audio on Demand. |
   | `AUDIOBOOK` | Streamtyp für Hörbuch. |
   | `PODCAST` | Streamtyp für Podcast. |

   **`MediaType`Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `Audio` | Medientyp für Audiostreams. |
   | `Video` | Medientyp für Videostreams. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Anhängen von Metadaten**

   Fügen Sie optional standardmäßige und/oder benutzerdefinierte Metadatenobjekte über Kontextdatenvariablen an die Verfolgungssitzung an.

   * **Standardmetadaten**

      [Standard-Metadaten in JavaScript implementieren](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Das Hinzufügen des Standard-Metadatenobjekts zum Medienobjekt ist optional.

      * Medien-Metadatenschlüssel API-Referenz: [Standard-Metadatenschlüssel - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und füllen Sie die Daten für diese Medien aus. Beispiel:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Verfolgen Sie die Absicht, die Wiedergabe zu starten.**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

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

1. **Verfolgen der tatsächlichen Wiedergabe**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Rückverfolgung der Wiedergabe**

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
   >`trackSessionEnd` markiert das Ende einer Verfolgungssitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Verfolgen Sie alle möglichen Pausenereignisse.**

   Identify the event from the media player for pause and call `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Anhalten-Szenarios**

   Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Anwender betätigt in der App die Pause-Schaltfläche.
   * Der Player geht selbstständig in den Pausenstatus über.
   * (*Mobile Apps*): Der Anwender setzt die App in den Hintergrund, Sie möchten die Sitzung jedoch geöffnet halten.
   * (*Mobile Apps*): Es tritt eine Systemunterbrechung auf, die dafür sorgt, dass die Anwendung im Hintergrund ausgeführt wird. Wenn der Anwender beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Anwender das Medium fortsetzen kann.

1. Identify the event from the player for play and/or resume from pause and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Dies kann dieselbe Ereignisquelle sein, die in Schritt 4 verwendet wurde. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* Tracking-Szenarios: [VOD-Wiedergabe ohne Werbung](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Der im JavaScript-SDK enthaltene Beispiel-Player zeigt ein komplettes Tracking-Beispiel.

