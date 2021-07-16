---
title: Erfahren Sie, wie Sie die Core-Wiedergabe in Roku verfolgen
description: Erfahren Sie, wie Sie das Core-Tracking mit dem Media SDK in Roku implementieren.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 97%

---

# Tracking von Core-Wiedergaben auf Roku{#track-core-playback-on-roku}

Diese Dokumentation behandelt das Tracking in der Version 2.x des SDK.

>[!IMPORTANT]
>Wenn Sie Version 1.x des SDK implementieren möchten, können Sie sich hier die Entwicklerhandbücher herunterladen: [SDKs herunterladen](/help/sdk-implement/download-sdks.md)

1. **Tracking-Ersteinrichtung**

   Identifizieren Sie, wenn der Benutzer die Wiedergabe auslöst (Benutzer klickt auf „Abspielen“ und/oder die automatische Wiedergabe ist aktiviert), und erstellen Sie eine `MediaObject`-Instanz.

   **`MediaObject`-Referenz:**

   | Variablenname | Beschreibung | erforderlich |
   | --- | --- | :---: |
   | `name` | Videoname | Ja |
   | `mediaid` | Eindeutige ID des Videos | Ja |
   | `length` | Videolänge | Ja |
   | `streamType` | Streamtyp (siehe _StreamType-Konstanten_ unten) | Ja |
   | `mediaType` | Medientyp (siehe _MediaType-Konstanten_ unten) | Ja |

   **`StreamType`-Konstanten:**

   | Konstantenname | Beschreibung   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Streamtyp für Video on Demand |
   | `MEDIA_STREAM_TYPE_LIVE` | Streamtyp für Live-Inhalt |
   | `MEDIA_STREAM_TYPE_LINEAR` | Streamtyp für Linear-Inhalt |
   | `MEDIA_STREAM_TYPE_AOD` | Streamtyp für Audio on Demand |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Streamtyp für Hörbuch |
   | `MEDIA_STREAM_TYPE_PODCAST` | Streamtyp für Podcast |

   **`MediaType`-Konstanten:**

   | Konstantenname | Beschreibung |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Medientyp für Audiostreams. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Medientyp für Videostreams. |

   **Erstellen Sie ein Medieninformationsobjekt für Videos mit VOD-Inhalt:**

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

   **Erstellen Sie ein Medieninformationsobjekt für Videos mit AOD-Inhalt:**

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

1. **Metadaten anhängen**

   Optional können Standard- bzw. benutzerdefinierte Metadatenobjekte über Kontextdatenvariablen an die Tracking-Sitzung angehängt werden.

   * **Standard-Metadaten**

[Standard-Metadaten in Roku implementieren](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Das Anhängen des Standard-Video-Metadatenobjekts an das Medienobjekt ist optional.

   * **Benutzerspezifische Metadaten**

      Erstellen Sie ein Variablenobjekt für die benutzerdefinierten Variablen und fügen Sie die Daten für dieses Video ein. Beispiel:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Absicht, die Wiedergabe zu starten, verfolgen**

   Rufen Sie `trackSessionStart` in der Media Heartbeat-Instanz auf, um eine Mediensitzung zu verfolgen:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >Der zweite Wert ist der Name des benutzerdefinierten Video-Metadatenobjekts, den Sie in Schritt 2 erstellt haben.

   >[!IMPORTANT]
   >`trackSessionStart` verfolgt die Absicht des Benutzers, die Wiedergabe zu starten, und nicht den Anfang der Wiedergabe. Mit dieser API können Sie die Videodaten/-Metadaten laden und die QoS-Metrik zur Ladezeit (zeitlicher Abstand zwischen `trackSessionStart` () und `trackPlay`) schätzen.

   >[!NOTE]
   >Wenn Sie keine benutzerdefinierten Video-Metadaten verwenden, senden Sie einfach ein leeres Objekt für das `data`-Argument in `trackSessionStart`, wie in der Kommentarzeile im obigen iOS-Beispiel gezeigt.

1. **Tatsächlichen Wiedergabebeginn verfolgen**

   Identifizieren Sie das Ereignis für den Anfang der Videowiedergabe im Videoplayer (wenn das erste Videobild auf dem Bildschirm angezeigt wird) und rufen Sie `trackPlay` () auf:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Ende der Wiedergabe verfolgen**

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
   >`trackSessionEnd` markiert das Ende einer Video-Tracking-Sitzung. Wenn die Sitzung erfolgreich bis zum Ende wiedergegeben wurde und der Anwender den Inhalt bis zum Schluss angesehen hat, müssen Sie `trackComplete` vor `trackSessionEnd` aufrufen. Jeder andere `track*`-API-Aufruf nach `trackSessionEnd` wird ignoriert, mit Ausnahme von `trackSessionStart` für eine neue Video-Tracking-Sitzung.

1. **Alle möglichen Pausenszenarien verfolgen**

   Identifizieren Sie das Ereignis im Videoplayer für angehaltene Videos und rufen Sie `trackPause` auf:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausenszenarien**

   Identifizieren Sie alle Szenarios, in denen der Videoplayer angehalten wird, und stellen Sie sicher, dass `trackPause` korrekt aufgerufen wird. In allen folgenden Szenarios muss Ihre App `trackPause()` () aufrufen:

   * Der Benutzer drückt in der App die Pausetaste.
   * Die Wiedergabe wird vom Player selbst pausiert.
   * (*Mobile Apps*) - Der Benutzer bewegt die App in den Hintergrund, aber Sie möchten, dass die Sitzung der App geöffnet bleibt.
   * (*Mobile Apps*) - Eine beliebige Systemunterbrechung tritt ein, die dazu führt, dass eine App im Hintergrund ausgeführt wird. Wenn der Benutzer beispielsweise einen Anruf erhält oder eine Popup-Nachricht einer anderen App angezeigt wird, die Anwendung die Sitzung jedoch aktiv halten soll, damit der Benutzer das Video fortsetzen kann.

1. Identifizieren Sie das Ereignis aus dem Player bei wiedergegebenen und/oder nach einer Pause wiederaufgenommenen Videos und rufen Sie `trackPlay` auf:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Diese Ereignisquelle kann mit der in Schritt 4 verwendeten identisch sein. Stellen Sie sicher, dass jeder `trackPause()`-API-Aufruf mit einem nachfolgenden `trackPlay()`-API-Aufruf gepaart wird, wenn die Videowiedergabe wiederaufgenommen wird.

* Tracking-Szenarien: [VOD-Wiedergabe ohne Anzeigen](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Der im Roku-SDK enthaltene Beispiel-Player zeigt ein komplettes Tracking-Beispiel.
