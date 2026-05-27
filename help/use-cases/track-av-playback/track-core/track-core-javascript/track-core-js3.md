---
title: Erfahren Sie, wie Sie die Core-Wiedergabe mit JavaScript v3.x verfolgen.
description: Erfahren Sie, wie Sie das Core-Tracking mit dem Media SDK in einem Browser mit JavaScript 3.x-Apps implementieren können.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/bIOfr94Q7wJLH9LfRg9VLIEJuS6JPvcgSWS62YCVguc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 85%

---

# Nachverfolgen der grundlegenden Wiedergabe mit JavaScript 3.x{#track-core-playback-on-javascript}

Diese Dokumentation behandelt das Tracking in der Version 3.x des SDK.

>[!IMPORTANT]
>
>Wenn Sie vorherige Versionen des SDK implementieren möchten, können Sie hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](/help/getting-started/download-sdks.md)

1. **Tracking-Ersteinrichtung**

   Identifizieren Sie, wenn der Benutzer die Wiedergabe auslöst (Benutzer klickt auf „Abspielen“ und/oder die automatische Wiedergabe ist aktiviert), und erstellen Sie eine `MediaObject`-Instanz.

   [createMediaObject-API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Variablenname | Typ | Beschreibung |
   | --- | --- | --- |
   | `name` | string | Nicht leere Zeichenfolge, die den Mediennamen angibt. |
   | `id` | string | Nicht leere Zeichenfolge, die die eindeutige Medienkennung angibt. |
   | `length` | number | Positive Zahl, die die Länge des Mediums in Sekunden angibt. Verwenden Sie 0, wenn die Länge unbekannt ist. |
   | `streamType` | string |   |
   | `mediaType` | | Medientyp (Audio oder Video). |

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

   Optional können standardmäßige bzw. benutzerdefinierte Metadaten über Kontextdatenvariablen an die Tracking-Sitzung angehängt werden.

   * **Standard-Metadaten**

     >[!NOTE]
     >
     >Das Anhängen der Standardmetadaten ist optional.

      * Medien-Metadatenschlüssel API-Referenz: [Standard-Metadatenschlüssel - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

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
   >Wenn Sie keine contextData verwenden, senden Sie einfach ein leeres Objekt für das `data`-Argument in `trackSessionStart`.

1. **Tatsächlichen Wiedergabebeginn verfolgen**

   Identifizieren Sie das Ereignis für den Anfang der Wiedergabe im Medienplayer, sobald der erste Frame des Mediums auf dem Bildschirm angezeigt wird, und rufen Sie `trackPlay` auf:

   ```js
   tracker.trackPlay();
   ```

1. **Abspielkopfwert aktualisieren**

   Wenn sich der Abspielkopf des Mediums ändert, informieren Sie die SDK durch Aufruf der `mediaUpdatePlayhead`-API. <br /> Bei Video-on-demand (VOD) wird der Wert in Sekunden ab Beginn des Medienelements angegeben. <br /> Wenn der Player beim Live-Streaming keine Informationen zur Inhaltsdauer bereitstellt, kann der Wert als Anzahl der Sekunden seit Mitternacht (UTC) des Tages angegeben werden.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Beachten Sie beim Aufrufen der `tracker.updatePlayhead`-API Folgendes:
   >* Bei Verwendung von Fortschrittsmarken ist die Inhaltsdauer erforderlich und der Abspielkopf muss als Anzahl von Sekunden ab Beginn des Medienelements aktualisiert werden, beginnend mit 0.
   >* Bei Verwendung von Medien-SDKs müssen Sie die `tracker.updatePlayhead`-API mindestens einmal pro Sekunde aufrufen.

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

* Tracking-Szenarien: [VOD-Wiedergabe ohne Anzeigen](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript-SDK mit Beispiel-Player für ein vollständiges Tracking-Beispiel.
