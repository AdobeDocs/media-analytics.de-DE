---
title: Einrichten des Media SDK in Android
description: Führen Sie diese Schritte aus, um das Media SDK-Programm unter Android einzurichten.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 97%

---

# Android einrichten{#set-up-android}

Erfahren Sie, wie Sie die Streaming-Mediensammlung für Android-Geräte einrichten.

>[!IMPORTANT]
>
>Ab dem 31. August 2021, dem Ende der Unterstützung für Mobile-SDKs der Version 4, stellt Adobe auch die Unterstützung für das Media Analytics-SDK für iOS und Android ein.  Weitere Informationen finden Sie unter den [häufig gestellten Fragen zum Ende der Unterstützung für das Media Analytics-SDK](/help/additional-resources/end-of-support-faqs.md).


## Voraussetzungen

* **Gültige Konfigurationsparameter für Media SDK festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **ADBMobile für Android in Ihre Anwendung implementieren:** Weitere Informationen zur Adobe Mobile-SDK-Dokumentation finden Sie unter [Android-SDK 4.x für Experience Cloud-Lösungen.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=de)

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
