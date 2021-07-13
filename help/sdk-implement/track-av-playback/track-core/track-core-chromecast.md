---
title: Erfahren Sie, wie Sie die Core-Wiedergabe in Chromecast verfolgen
description: Erfahren Sie, wie Sie das Core-Tracking mit dem Media SDK in Chromecast implementieren.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 96%

---

# Tracking von Core-Wiedergaben auf Chromecast{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>Diese Dokumentation behandelt das Tracking in der Version 2.x des SDK. Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](/help/sdk-implement/download-sdks.md)

1. **Tracking-Ersteinrichtung**

   Identifizieren Sie, wenn der Benutzer die Wiedergabe auslöst (Benutzer klickt auf „Abspielen“ und/oder die automatische Wiedergabe ist aktiviert), und erstellen Sie eine `MediaObject`-Instanz.

   **`MediaObject`API-Referenz:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`-Konstanten:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`-Konstanten:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Video-Metadaten anhängen**

   Optional können Standard- bzw. benutzerdefinierte Video-Metadatenobjekte über Kontextdatenvariablen an die Video-Tracking-Sitzung angehängt werden.

   * **Standard-Video-Metadaten**

      [Standard-Metadaten in Chromecast implementieren](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >Das Anhängen des Standard-Video-Metadatenobjekts an das Medienobjekt ist optional.

   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und fügen Sie die Daten für dieses Video ein. Beispiel:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Absicht, die Wiedergabe zu starten, verfolgen**

   Rufen Sie [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) im `media`-Objekt auf, um eine Mediensitzung zu verfolgen.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Videodaten/-Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >
   >Der zweite Wert ist der Name des benutzerdefinierten Video-Metadatenobjekts, den Sie in Schritt 2 erstellt haben. Wenn Sie keine benutzerdefinierten Video-Metadaten verwenden, senden Sie einfach ein leeres Objekt für das `data`-Argument in `trackSessionStart`, wie in der Kommentarzeile im obigen iOS-Beispiel gezeigt.

1. **Tatsächlichen Wiedergabebeginn verfolgen**

   Identifizieren Sie das Ereignis für den Anfang der Videowiedergabe im Videoplayer, sobald der erste Frame des Videos auf dem Bildschirm angezeigt wird, und rufen Sie [trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay) auf:

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Ende der Wiedergabe verfolgen**

   Identifizieren Sie das Ereignis für den Abschluss der Videowiedergabe im Videoplayer, wenn der Inhalt bis zum Ende angesehen wurde, und rufen Sie [trackComplete](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete) auf:

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Ende der Sitzung verfolgen**

   Identifizieren Sie das Ereignis für das Entladen/Schließen der Videowiedergabe im Videoplayer, wenn der Benutzer das Video schließt bzw. das Video abgeschlossen ist und entladen wird, und rufen Sie [trackSessionEnd](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd) auf:

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markiert das Ende einer Video-Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Jeder andere `track*`-API-Aufruf nach `trackSessionEnd` wird ignoriert, mit Ausnahme von `trackSessionStart` für eine neue Video-Tracking-Sitzung.

1. **Alle möglichen Pausenszenarien verfolgen**

   Identifizieren Sie das Ereignis im Videoplayer für angehaltene Videos und rufen Sie [trackPause](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause) auf:

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausenszenarien**

   Identifizieren Sie alle Szenarios, in denen der Videoplayer angehalten wird, und stellen Sie sicher, dass `trackPause` korrekt aufgerufen wird. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Benutzer drückt in der App die Pausetaste.
   * Die Wiedergabe wird vom Player selbst pausiert.
   * (*Mobile Apps*) - Der Benutzer bewegt die App in den Hintergrund, aber Sie möchten, dass die Sitzung der App geöffnet bleibt.
   * (*Mobile Apps*) - Eine beliebige Systemunterbrechung tritt ein, die dazu führt, dass eine App im Hintergrund ausgeführt wird. Wenn der Benutzer beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Benutzer das Video fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei wiedergegebenen und/oder nach einer Pause wiederaufgenommenen Videos und rufen Sie [trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete) auf:

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Diese Ereignisquelle kann mit der in Schritt 4 verwendeten identisch sein. Stellen Sie sicher, dass jeder `trackPause()`-API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Videowiedergabe wiederaufgenommen wird.

* Tracking-Szenarien: [VOD-Wiedergabe ohne Anzeigen](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Der im Chromecast-SDK enthaltene Beispiel-Player zeigt ein komplettes Tracking-Beispiel.
