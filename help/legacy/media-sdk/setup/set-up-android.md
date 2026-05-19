---
title: Einrichten des Media SDK in Android
description: Führen Sie diese Schritte aus, um das Media SDK-Programm unter Android einzurichten.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/re7nZLD9IwvufJGicWLArSwdIi6h518q3ZMDf6oqaCI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 86%

---

# Android einrichten{#set-up-android}

Erfahren Sie, wie Sie Streaming-Mediendienste für Android-Geräte einrichten.

>[!IMPORTANT]
>
>Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein.  Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/additional-resources/end-of-support-faqs.md).


## Voraussetzungen

* **Abrufen gültiger Konfigurationsparameter für die Media SDK**
Sie können diese Parameter von einem Adobe-Support-Mitarbeiter erhalten, nachdem Sie Ihr Analytics-Konto eingerichtet haben.
* **Implementieren von ADBMobile für Android in Ihrer Anwendung**
Weitere Informationen zur Dokumentation zu Adobe Mobile SDK finden Sie unter [Android SDK 4.x for Experience Cloud Solutions.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=de)

* **Stellen Sie die folgenden Funktionen in Ihrem Medienplayer bereit:**
   * *Eine API zum Abonnieren von Player-Ereignissen*: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * *Eine API, die Player-Informationen bereitstellt*: Diese Informationen enthalten Details wie den Mediennamen und die Abspielposition.

## SDK-Implementierung

1. Fügen Sie Ihr heruntergeladenes Medien-SDK zu Ihrem Projekt hinzu.

   1. Erweitern Sie die Android-Zip-Datei (z. B. `MediaSDK-android-v2.*.zip`).
   1. Stellen Sie sicher, dass die Datei `MediaSDK.jar` im Verzeichnis `libs/` vorhanden ist.

   1. Fügen Sie die Bibliothek zu Ihrem Projekt hinzu.

      **IntelliJ IDEA:**

      1. Klicken Sie im Bereich **[!UICONTROL Projektnavigation]** mit der rechten Maustaste auf Ihr Projekt.
      1. Wählen Sie **[!UICONTROL Moduleinstellungen öffnen]**.
      1. Wählen Sie unter **[!UICONTROL Projekteinstellungen]** die Option **[!UICONTROL Bibliotheken]**.

      1. Klicken Sie auf **[!UICONTROL +]**, um eine neue Bibliothek hinzuzufügen.
      1. Wählen Sie **[!UICONTROL Java]** und navigieren Sie zur Datei `MediaSDK.jar`.

      1. Wählen Sie die Module aus, in denen Sie die Mobile-Bibliothek verwenden möchten.
      1. Klicken Sie auf **[!UICONTROL Anwenden]** und dann auf **[!UICONTROL OK]**, um das Moduleinstellungsfenster zu schließen.

      **Eclipse:**

      1. Klicken Sie in der Eclipse IDE mit der rechten Maustaste auf den Projektnamen.
      1. Klicken Sie auf **[!UICONTROL Pfad aufbauen]** > **[!UICONTROL Externe Archive hinzufügen]** .
      1. Auswählen `MediaSDK.jar`.
      1. Klicken Sie auf **[!UICONTROL Öffnen]**.
      1. Klicken Sie erneut mit der rechten Maustaste auf das Projekt und klicken Sie dann auf  **[!UICONTROL Pfad aufbauen]** > **[!UICONTROL Pfadaufbau konfigurieren]**.
      1. Klicken Sie auf die Tabs **[!UICONTROL Sortierung]** und **[!UICONTROL Export]**.

      1. Stellen Sie sicher, dass die Datei `MediaSDK.jar` ausgewählt ist.

1. Importieren Sie die Bibliothek.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Erstellen Sie die `MediaHeartbeatConfig`-Instanz.

   Hier finden Sie eine Beispielinitialisierung für `MediaHeartbeatConfig`:

   ```java
   // Media Heartbeat Initialization
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_;
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName = <SAMPLE_PLAYER_NAME>;
   config.ssl = <true/false>;
   config.debugLogging = <true/false>;
   ```

1. Implementieren Sie die `MediaHeartbeatDelegate`-Schnittstelle.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override
   public MediaObject getQoSObject() {
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>);
   }
   
   //Replace <currentPlaybackTime> with the video player current playback time
   @Override
   public Double getCurrentPlaybackTime() {
       return <currentPlaybackTime>;
   }
   ```

1. Erstellen Sie die `MediaHeartbeat`-Instanz.

   Verwenden Sie die `MediaHeartbeatConfig`- und die `MediaHertbeatDelegate`-Instanz, um die `MediaHeartbeat`-Instanz zu erstellen.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass die `MediaHeartbeat`-Instanz zugänglich ist und ihre Zuweisung *nicht vor Ende der Sitzung aufgehoben wird*. Diese Instanz wird für alle der folgenden-Tracking-Ereignisse verwendet.

**Hinzufügen von App-Berechtigungen**

Ihre App, die das Media SDK verwendet, benötigt die folgenden Berechtigungen, um Daten bei Tracking-Aufrufen zu senden:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Ergänzen Sie die Datei `AndroidManifest.xml` im Projektverzeichnis der Anwendung um die folgenden Zeilen, um diese Berechtigungen hinzuzufügen:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migration von Version 1.x auf 2.x in Android**

In den Versionen 2.x sind alle öffentlichen Methoden in der Klasse `com.adobe.primetime.va.simple.MediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern. Außerdem sind alle Konfigurationen nun in der `com.adobe.primetime.va.simple.MediaHeartbeatConfig`-Klasse konsolidiert.

Informationen über die Migration von 1.x auf 2.x finden Sie in der Dokumentation zur Legacy-Implementierung.
