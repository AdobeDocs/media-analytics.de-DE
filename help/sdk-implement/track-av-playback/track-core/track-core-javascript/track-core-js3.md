---
title: Core-Wiedergabe mit JavaScript v3.x verfolgen
description: In diesem Thema wird beschrieben, wie Sie die Kernverfolgung mit dem Media SDK in einem Browser implementieren, der JavaScript 3.x-Apps verwendet.
translation-type: tm+mt
source-git-commit: 40d75ef32596e915ac07c173b4595bb78db3688d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 81%

---


# Core-Wiedergabe mit JavaScript 3.x verfolgen{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Diese Dokumentation behandelt das Tracking in der Version 3.x des SDK. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs](/help/sdk-implement/download-sdks.md)

1. **Tracking-Ersteinrichtung**

   Identifizieren Sie, wenn der Benutzer die Wiedergabe auslöst (Benutzer klickt auf „Abspielen“ und/oder die automatische Wiedergabe ist aktiviert), und erstellen Sie eine `MediaObject`-Instanz.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Variablenname | Typ | Beschreibung |
   | --- | --- | --- |
   | `name` | string | Nicht leere Zeichenfolge, die den Mediennamen angibt. |
   | `id` | string | Nicht leere Zeichenfolge, die die eindeutige Medienkennung angibt. |
   | `length` | Anzahl | Positive Zahl, die die Länge des Mediums in Sekunden angibt. Verwenden Sie 0, wenn die Länge unbekannt ist. |
   | `streamType` | string |  |
   | `mediaType` |  | Medientyp (Audio oder Video). |

   **`StreamType`-Konstanten:**

   | Konstantenname | Beschreibung   |
   |---|---|
   | `VOD` | Streamtyp für Video on Demand |
   | `AOD` | Streamtyp für Audio on Demand. |

   **`MediaType`-Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `Audio` | Medientyp für Audiostreams. |
   | `Video` | Medientyp für Videostreams. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Metadaten anhängen**

   Fügen Sie der Tracking-Sitzung optional Standard- und/oder benutzerdefinierte Metadaten über Kontextdatenvariablen hinzu.

   * **Standard-Metadaten**

      >[!NOTE]
      >
      >Das Anhängen der Standardmetadaten ist optional.

      * Medien-Metadatenschlüssel API-Referenz: [Standard-Metadatenschlüssel - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Hier sehen Sie den umfassenden Satz der verfügbaren Metadaten: [Audio- und Videoparameter](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und fügen Sie die Daten für dieses Medium ein. Beispiel:

      ```js
      /* Set context data */
       var contextData = {};
      
       //Standard metadata
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
      
       //Custom metadata
       contextData["isUserLoggedIn"] = "false";
       contextData["tvStation"] = "Sample TV Station";
      ```


1. **Absicht, die Wiedergabe zu starten, verfolgen**

   Rufen Sie `trackSessionStart` in der Media Heartbeat-Instanz auf, um eine Mediensitzung zu verfolgen:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Daten/Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >If you are not using contextData, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Tatsächlichen Wiedergabebeginn verfolgen**

   Identifizieren Sie das Ereignis für den Anfang der Wiedergabe im Medienplayer, sobald der erste Frame des Mediums auf dem Bildschirm angezeigt wird, und rufen Sie `trackPlay` auf:

   ```js
   tracker.trackPlay();
   ```

1. **Ende der Wiedergabe verfolgen**

   Identifizieren Sie das Ereignis für den Abschluss der Wiedergabe im Medienplayer, wenn der Inhalt bis zum Ende angesehen wurde, und rufen Sie `trackComplete` auf:

   ```js
   tracker.trackComplete();
   ```

1. **Ende der Sitzung verfolgen**

   Identifizieren Sie das Ereignis für das Entladen/Schließen der Wiedergabe im Medienplayer, wenn der Benutzer das Medium schließt bzw. das Medium abgeschlossen ist und entladen wird, und rufen Sie `trackSessionEnd` auf:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markiert das Ende einer Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Jeder andere `track*`-API-Aufruf nach `trackSessionEnd` wird ignoriert, mit Ausnahme von `trackSessionStart` für eine neue Tracking-Sitzung.

1. **Alle möglichen Pausenszenarien verfolgen**

   Identifizieren Sie das Ereignis im Medienplayer für Anhalten und rufen Sie `trackPause` auf:

   ```js
   tracker.trackPause();
   ```

   **Pausenszenarien**

   Identifizieren Sie alle Szenarios, in denen der Medienplayer angehalten wird, und stellen Sie sicher, dass `trackPause` korrekt aufgerufen wird. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Benutzer drückt in der App die Pausetaste.
   * Die Wiedergabe wird vom Player selbst pausiert.
   * (*Mobile Apps*) - Der Benutzer bewegt die App in den Hintergrund, aber Sie möchten, dass die Sitzung der App geöffnet bleibt.
   * (*Mobile Apps*) - Eine beliebige Systemunterbrechung tritt ein, die dazu führt, dass eine App im Hintergrund ausgeführt wird. Beispielsweise erhält der Benutzer einen Anruf oder ein Pop-up aus einer anderen App, aber Sie möchten, dass die App-Sitzung fortgeführt wird, damit der Benutzer die Medien ab dem Zeitpunkt der Unterbrechung wieder fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei Wiedergabe und/oder Fortsetzen nach Pause und rufen Sie `trackPlay` auf:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Diese Ereignisquelle kann mit der in Schritt 4 verwendeten identisch sein. Stellen Sie sicher, dass jeder `trackPause()`API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Wiedergabe fortgesetzt wird.

* Tracking-Szenarien: [VOD-Wiedergabe ohne Anzeigen](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript-SDK mit Beispiel-Player für ein vollständiges Tracking-Beispiel.