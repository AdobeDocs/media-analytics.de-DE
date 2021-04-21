---
title: Tracking von Core-Wiedergaben auf iOS
description: Hier wird die Implementierung des Core-Trackings mit dem Media SDK in iOS beschrieben.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '712'
ht-degree: 100%

---

# Tracking von Core-Wiedergaben auf iOS {#track-core-playback-on-ios}

>[!IMPORTANT]
>Diese Dokumentation behandelt das Tracking in der Version 2.x des SDK. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](/help/sdk-implement/download-sdks.md)

1. **Tracking-Ersteinrichtung**

   Identifizieren Sie, wenn der Benutzer die Wiedergabe auslöst (Benutzer klickt auf „Abspielen“ und/oder die automatische Wiedergabe ist aktiviert), und erstellen Sie eine `MediaObject`-Instanz.

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Variablenname | Beschreibung | erforderlich |
   |---|---|---|
   | `name` | Videoname | Ja |
   | `mediaid` | Eindeutige ID des Videos | Ja |
   | `length` | Videolänge | Ja |
   | `streamType` | Streamtyp (siehe _StreamType-Konstanten_ unten) | Ja |
   | `mediaType` | Medientyp (siehe _MediaType-Konstanten_ unten) | Ja |

   **`StreamType`-Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Streamtyp für Video on Demand |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Streamtyp für Live-Inhalt |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Streamtyp für Linear-Inhalt |
   | `ADBMediaHeartbeatStreamTypeAOD` | Streamtyp für Audio on Demand |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Streamtyp für Hörbuch |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Streamtyp für Podcast |

   **`MediaType`-Konstanten:**

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

1. **Video-Metadaten anhängen**

   Optional können Standard- bzw. benutzerdefinierte Video-Metadatenobjekte über Kontextdatenvariablen an die Video-Tracking-Sitzung angehängt werden.

   * **Standard-Video-Metadaten**

      * [Standard-Metadaten in iOS implementieren](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Schlüssel für Video-Metadaten**

         [iOS-Metadataschlüssel](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Sehen Sie hier die umfassende Liste der verfügbaren Video-Metadaten: [Audio- und Videoparameter](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >Das Anhängen des Standard-Video-Metadatenobjekts an das Medienobjekt ist optional.

   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und fügen Sie die Daten für dieses Video ein. Beispiel:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Absicht, die Wiedergabe zu starten, verfolgen**

   Rufen Sie `trackSessionStart` in der Media Heartbeat-Instanz auf, um eine Mediensitzung zu verfolgen.

   >[!TIP]
   >
   >Der zweite Wert ist der Name des benutzerdefinierten Video-Metadatenobjekts, den Sie in Schritt 2 erstellt haben.

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
   >Wenn Sie keine benutzerdefinierten Video-Metadaten verwenden, senden Sie einfach ein leeres Objekt für das `data`-Argument in `trackSessionStart`, wie in der Kommentarzeile im obigen iOS-Beispiel gezeigt.

1. **Tatsächlichen Wiedergabebeginn verfolgen**

   Identifizieren Sie das Ereignis für den Anfang der Videowiedergabe im Videoplayer (wenn das erste Videobild auf dem Bildschirm angezeigt wird) und rufen Sie `trackPlay` () auf:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Ende der Wiedergabe verfolgen**

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
   >`trackSessionEnd` markiert das Ende einer Video-Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Jeder andere `track*`-API-Aufruf nach `trackSessionEnd` wird ignoriert, mit Ausnahme von `trackSessionStart` für eine neue Video-Tracking-Sitzung.

1. **Alle möglichen Pausenszenarien verfolgen**

   Identifizieren Sie das Ereignis im Videoplayer für angehaltene Videos und rufen Sie `trackPause` auf:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Pausenszenarien**

   Identifizieren Sie alle Szenarios, in denen der Videoplayer angehalten wird, und stellen Sie sicher, dass `trackPause` korrekt aufgerufen wird. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Benutzer drückt in der App die Pausetaste.
   * Die Wiedergabe wird vom Player selbst pausiert.
   * (*Mobile Apps*) - Der Benutzer bewegt die App in den Hintergrund, aber Sie möchten, dass die Sitzung der App geöffnet bleibt.
   * (*Mobile Apps*) - Eine beliebige Systemunterbrechung tritt ein, die dazu führt, dass eine App im Hintergrund ausgeführt wird. Wenn der Benutzer beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Benutzer das Video fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei wiedergegebenen und/oder nach einer Pause wiederaufgenommenen Videos und rufen Sie `trackPlay` auf:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >Diese Ereignisquelle kann mit der in Schritt 4 verwendeten identisch sein. Stellen Sie sicher, dass jeder `trackPause()`-API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Videowiedergabe wiederaufgenommen wird.

Im Folgenden finden Sie weitere Informationen zum Tracking der Core-Wiedergabe:

* Tracking-Szenarien: [VOD-Wiedergabe ohne Anzeigen](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Der im iOS-SDK enthaltene Beispiel-Player zeigt ein komplettes Tracking-Beispiel.
