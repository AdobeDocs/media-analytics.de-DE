---
title: Tracking von Core-Wiedergaben auf Android
description: In diesem Thema wird beschrieben, wie Sie die Kernverfolgung mit dem Media SDK unter Android implementieren.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracking von Core-Wiedergaben auf Android{#track-core-playback-on-android}

>[!IMPORTANT]
>Diese Dokumentation behandelt die Verfolgung in Version 2.x des SDK. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie hier das 1.x-Entwicklerhandbuch für Android herunterladen: [SDKs herunterladen](/help/sdk-implement/download-sdks.md).

1. **Einrichtung der anfänglichen Verfolgung**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Medienname | Ja |
   | `mediaId` | Eindeutige Medienkennung | Ja |
   | `length` | Medienlänge | Ja |
   | `streamType` | Stream-Typ (siehe _StreamType-Konstanten_ unten) | Ja |
   | `mediaType` | Medientyp (siehe _MediaType-Konstanten_ unten) | Ja |

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

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Anhängen von Metadaten**

   Fügen Sie der Verfolgungssitzung optional Standard- und/oder benutzerdefinierte Metadatenobjekte über Kontextdatenvariablen hinzu.

   * **Standard-Metadaten**

      [Standard-Metadaten in Android implementieren](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >Das Anhängen des Standard-Metadatenobjekts an das Medienobjekt ist optional.

      * Medien-Metadatenschlüssel API-Referenz: [Standard-Metadatenschlüssel - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Hier sehen Sie den umfassenden Satz der verfügbaren Video-Metadaten: [Audio- und Videoparameter](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Wörterbuch für die benutzerdefinierten Variablen und füllen Sie die Daten für dieses Medium aus. Beispiel:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Verfolgung der Absicht, die Wiedergabe zu starten**

   Rufen Sie zur Verfolgung einer Mediensitzung die Media Heartbeat-Instanz `trackSessionStart` auf. Beispiel:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >Der zweite Wert ist der benutzerdefinierte Medienmetadatenobjektname, den Sie in Schritt 2 erstellt haben.

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Mediendaten/-Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **Den tatsächlichen Start der Wiedergabe verfolgen**

   Identify the event from the media player for the beginning of the media playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Verfolgen Sie den Abschluss der Wiedergabe.**

   Identify the event from the media player for the completion of the media playback, where the user has watched the content until the end, and call `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Ende der Sitzung verfolgen**

   Identify the event from the media player for the unloading/closing of the media playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markiert das Ende einer Medienverfolgungssitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **Alle möglichen Pausenszenarien verfolgen**

   Identifizieren Sie das Ereignis für Medienpause und -aufruf im Medienplayer `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Szenarios anhalten**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Anwender betätigt in der App die Pause-Schaltfläche.
   * Der Player geht selbstständig in den Pausenstatus über.
   * (*Mobile Apps*): Der Anwender setzt die App in den Hintergrund, Sie möchten die Sitzung jedoch geöffnet halten.
   * (*Mobile Apps*): Es tritt eine Systemunterbrechung auf, die dafür sorgt, dass die Anwendung im Hintergrund ausgeführt wird. Wenn der Anwender beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Anwender das Medium fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei wiedergegebenen und/oder nach einer Pause wiederaufgenommenen Medien und rufen Sie `trackPlay` auf.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Dies kann dieselbe Ereignisquelle sein, die in Schritt 4 verwendet wurde. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

Im Folgenden finden Sie weitere Informationen zum Tracking der Core-Wiedergabe:

* Tracking-Szenarios: [VOD-Wiedergabe ohne Werbung](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Der im Android-SDK enthaltene Beispiel-Player zeigt ein komplettes Tracking-Beispiel.

