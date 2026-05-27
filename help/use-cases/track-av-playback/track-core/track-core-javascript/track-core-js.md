---
title: Erfahren Sie, wie Sie die Core-Wiedergabe mit JavaScript 2.x verfolgen.
description: Erfahren Sie, wie Sie das Core-Tracking mit dem Media SDK in einem Browser mit JavaScript 2.x-Anwendungen implementieren.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/efxauhuL5aOcMQhSuayeodzUOtgfppMgZTAiwTiHsEE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 693
ht-degree: 99%

---

# Nachverfolgen der grundlegenden Wiedergabe mit JavaScript 2.x{#track-core-playback-on-javascript}

Mit den folgenden Anweisungen können Sie die Implementierung der 2.x-SDKs vornehmen.

>[!IMPORTANT]
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](/help/getting-started/download-sdks.md)

1. **Tracking-Ersteinrichtung**

   Identifizieren Sie, wenn der Benutzer die Wiedergabe auslöst (Benutzer klickt auf „Abspielen“ und/oder die automatische Wiedergabe ist aktiviert), und erstellen Sie eine `MediaObject`-Instanz.

   [createMediaObject-API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Medienname | Ja |
   | `mediaid` | Eindeutige Medienkennung | Ja |
   | `length` | Medienlänge | Ja |
   | `streamType` | Streamtyp (siehe _StreamType-Konstanten_ unten) | Ja |
   | `mediaType` | Medientyp (siehe _MediaType-Konstanten_ unten) | Ja |

   **`StreamType`-Konstanten:**

   | Konstantenname | Beschreibung   |
   |---|---|
   | `VOD` | Streamtyp für Video on Demand |
   | `LIVE` | Streamtyp für Live-Inhalt |
   | `LINEAR` | Streamtyp für Linear-Inhalt |
   | `AOD` | Streamtyp für Audio on Demand. |
   | `AUDIOBOOK` | Streamtyp für Hörbuch. |
   | `PODCAST` | Streamtyp für Podcast. |

   **`MediaType`-Konstanten:**

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

1. **Metadaten anhängen**

   Optional können Standard- bzw. benutzerdefinierte Metadatenobjekte über Kontextdatenvariablen an die Tracking-Sitzung angehängt werden.

   * **Standard-Metadaten**

     [Standard-Metadaten in JavaScript implementieren](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

     >[!NOTE]
     >
     >Das Anhängen des Standard-Metadatenobjekts an das Medienobjekt ist optional.

      * Medien-Metadatenschlüssel API-Referenz: [Standard-Metadatenschlüssel - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

   * **Benutzerspezifische Metadaten**

     Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und fügen Sie die Daten für dieses Medium ein. Beispiel:

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Absicht, die Wiedergabe zu starten, verfolgen**

   Rufen Sie `trackSessionStart` in der Media Heartbeat-Instanz auf, um eine Mediensitzung zu verfolgen:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Der zweite Wert ist der Name des benutzerdefinierten Medienmetadatenobjekts, den Sie in Schritt 2 erstellt haben.

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Daten/Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >Wenn Sie keine benutzerdefinierten Metadaten verwenden, senden Sie einfach ein leeres Objekt für das `data`-Argument in `trackSessionStart`, wie in der Kommentarzeile im obigen iOS-Beispiel gezeigt.

1. **Tatsächlichen Wiedergabebeginn verfolgen**

   Identifizieren Sie das Ereignis für den Anfang der Wiedergabe im Medienplayer, sobald der erste Frame des Mediums auf dem Bildschirm angezeigt wird, und rufen Sie `trackPlay` auf:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Ende der Wiedergabe verfolgen**

   Identifizieren Sie das Ereignis für den Abschluss der Wiedergabe im Medienplayer, wenn der Inhalt bis zum Ende angesehen wurde, und rufen Sie `trackComplete` auf:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Ende der Sitzung verfolgen**

   Identifizieren Sie das Ereignis für das Entladen/Schließen der Wiedergabe im Medienplayer, wenn der Benutzer das Medium schließt bzw. das Medium abgeschlossen ist und entladen wird, und rufen Sie `trackSessionEnd` auf:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markiert das Ende einer Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Jeder andere `track*`-API-Aufruf nach `trackSessionEnd` wird ignoriert, mit Ausnahme von `trackSessionStart` für eine neue Tracking-Sitzung.

1. **Alle möglichen Pausenszenarien verfolgen**

   Identifizieren Sie das Ereignis im Medienplayer für Anhalten und rufen Sie `trackPause` auf:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pausenszenarien**

   Identifizieren Sie alle Szenarios, in denen der Medienplayer angehalten wird, und stellen Sie sicher, dass `trackPause` korrekt aufgerufen wird. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Benutzer drückt in der App die Pausetaste.
   * Die Wiedergabe wird vom Player selbst pausiert.
   * (*Mobile Apps*) - Der Benutzer bewegt die App in den Hintergrund, aber Sie möchten, dass die Sitzung der App geöffnet bleibt.
   * (*Mobile Apps*) - Eine beliebige Systemunterbrechung tritt ein, die dazu führt, dass eine App im Hintergrund ausgeführt wird. Beispielsweise erhält der Benutzer einen Anruf oder ein Pop-up aus einer anderen App, aber Sie möchten, dass die App-Sitzung fortgeführt wird, damit der Benutzer die Medien ab dem Zeitpunkt der Unterbrechung wieder fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei Wiedergabe und/oder Fortsetzen nach Pause und rufen Sie `trackPlay` auf:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Diese Ereignisquelle kann mit der in Schritt 4 verwendeten identisch sein. Stellen Sie sicher, dass jeder `trackPause()`API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Wiedergabe fortgesetzt wird.

* Tracking-Szenarien: [VOD-Wiedergabe ohne Anzeigen](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript-SDK mit Beispiel-Player für ein vollständiges Tracking-Beispiel.
