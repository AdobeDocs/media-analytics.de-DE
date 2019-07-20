---
seo-title: Tracking von Core-Wiedergaben auf iOS
title: Tracking von Core-Wiedergaben auf iOS
uuid: bdc 0 e 05 c -4 fe 5-430 e-aee 2-f 331 bc 59 ac 6 b
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Tracking von Core-Wiedergaben auf iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>Diese Dokumentation enthält die Verfolgung in Version 2. x des SDK. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](../../../sdk-implement/download-sdks.md)

1. **Initiales Tracking-Setup**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Variablenname | Beschreibung | erforderlich |
   |---|---|---|
   | `name` | Videoname | Ja |
   | `mediaid` | Eindeutige ID des Videos | Ja |
   | `length` | Videolänge | Ja |
   | `streamType` | Stream type (see _StreamType constants_ below) | Ja |
   | `mediaType` | Media type (see _MediaType constants_ below) | Ja |

   **`StreamType`Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Streamtyp für Video on Demand |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Streamtyp für Live-Inhalt |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Streamtyp für Linear-Inhalt |
   | `ADBMediaHeartbeatStreamTypeAOD` | Streamtyp für Audio on Demand |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Streamtyp für Hörbuch |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Streamtyp für Podcast |

   **`MediaType`Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `ADBMediaTypeAudio` | Medientyp für Audiostreams. |
   | `ADBMediaTypeVideo` | Medientyp für Videostreams. |

   Das allgemeine Format für die Erstellung des `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Anhängen von Videometadaten**

   Fügen Sie optional standardmäßige und/oder benutzerdefinierte Videometadatenobjekte über Kontextdatenvariablen an die Videoverfolgungssitzung an.

   * **Standard-Videometadaten**

      * [Standard-Metadaten in iOS implementieren](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Videometadatenschlüssel**
         [iOS-Metadataschlüssel](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Sehen Sie hier die umfassende Liste der verfügbaren Video-Metadaten: [Audio- und Videoparameter](../../../metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >Das Anhängen des Standard-Videometadatenobjekts an das Medienobjekt ist optional.

   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und füllen Sie die Daten für dieses Video aus. Beispiel:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Verfolgen Sie die Absicht, die Wiedergabe zu starten.**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance.

   >[!TIP]
   >
   >Der zweite Wert ist der benutzerdefinierte Videometadatenname, den Sie in Schritt 2 erstellt haben.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Videodaten/-Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Verfolgen der tatsächlichen Wiedergabe**

   Identifizieren Sie das Ereignis für den Anfang der Videowiedergabe im Videoplayer (wenn das erste Videobild auf dem Bildschirm angezeigt wird) und rufen Sie `trackPlay` () auf:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Rückverfolgung der Wiedergabe**

   Identifizieren Sie das Ereignis für den Abschluss der Videowiedergabe im Videoplayer (wenn der Inhalt bis zum Ende angesehen wurde) und rufen Sie `trackComplete` () auf:

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Ende der Sitzung verfolgen**

   Identifizieren Sie das Ereignis für das Entfernen/Schließen der Videowiedergabe im Videoplayer (wenn der Benutzer das Video schließt und/oder das Video abgeschlossen ist und aus dem Player entfernt wird) und rufen Sie `trackSessionEnd` () auf:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markiert das Ende einer Videoverfolgungssitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Verfolgen Sie alle möglichen Pausenereignisse.**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Anhalten-Szenarios**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Anwender betätigt in der App die Pause-Schaltfläche.
   * Der Player geht selbstständig in den Pausenstatus über.
   * (*Mobile Apps*): Der Anwender setzt die App in den Hintergrund, Sie möchten die Sitzung jedoch geöffnet halten.
   * (*Mobile Apps*): Es tritt eine Systemunterbrechung auf, die dafür sorgt, dass die Anwendung im Hintergrund ausgeführt wird. Wenn der Benutzer beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Benutzer das Video fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei wiedergegebenen und/oder nach einer Pause wiederaufgenommenen Videos und rufen Sie `trackPlay` auf:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >Dies kann dieselbe Ereignisquelle sein, die in Schritt 4 verwendet wurde. Stellen Sie sicher, dass jeder `trackPause()`-API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Videowiedergabe wiederaufgenommen wird.

Im Folgenden finden Sie weitere Informationen zum Tracking der Core-Wiedergabe:

* Tracking-Szenarios: [VOD-Wiedergabe ohne Werbung](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Der im iOS-SDK enthaltene Beispiel-Player zeigt ein komplettes Tracking-Beispiel.

