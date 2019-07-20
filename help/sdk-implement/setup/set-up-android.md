---
seo-title: Android einrichten
title: Android einrichten
uuid: 3 ffe 3276-a 104-4182-9220-038729 e 9 f 3 d 5
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Android einrichten{#set-up-android}

## Voraussetzungen

* **Beziehen Sie gültige Konfigurationsparameter für das Media SDK**
Diese Parameter können von einem Adobe-Vertreter erhalten werden, nachdem Sie Ihr Analytics-Konto eingerichtet haben.
* **Adbmobile for Android in Ihrer Anwendung**
implementieren. Weitere Informationen zur Adobe Mobile SDK-Dokumentation finden Sie unter [Android SDK 4. x für Experience Cloud-Lösungen.](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **Stellen Sie in Ihrem Medienplayer folgende Funktionen bereit:**
   * *Eine API, um Player-Ereignisse zu abonnieren:* Die Medien-SDK erfordert, dass Sie einige einfache APIs aufrufen, wenn Ereignisse in Ihrem Player auftreten.
   * *Eine API, die Playerinformationen bereitstellt:* Diese Informationen enthalten Details wie z. B. Medienname und Abspielposition.

## SDK-Implementierung

1. Fügen Sie Ihr [heruntergeladenes](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Medien-SDK zu Ihrem Projekt hinzu.

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. Fügen Sie die Bibliothek zu Ihrem Projekt hinzu.

      **IntelliJ IDEA:**

      1. Klicken Sie im Bereich **[!UICONTROL Projektnavigation]** mit der rechten Maustaste auf Ihr Projekt.
      1. Wählen Sie **[!UICONTROL Moduleinstellungen öffnen]**.
      1. Wählen Sie unter **[!UICONTROL Projekteinstellungen]** die Option **[!UICONTROL Bibliotheken]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Wählen Sie **[!UICONTROL Java]** und navigieren Sie zur Datei `MediaSDK.jar`.

      1. Wählen Sie die Module aus, in denen Sie die Mobile-Bibliothek verwenden möchten.
      1. Klicken Sie auf **[!UICONTROL Anwenden]** und dann auf **[!UICONTROL OK]**, um das Moduleinstellungsfenster zu schließen.
      **Eclipse:**

      1. Klicken Sie in der Eclipse IDE mit der rechten Maustaste auf den Projektnamen.
      1. Click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. Auswählen `MediaSDK.jar`.
      1. Klicken Sie auf **[!UICONTROL Öffnen]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. Klicken Sie auf die Tabs **[!UICONTROL Sortierung]** und **[!UICONTROL Export]**.

      1. Stellen Sie sicher, dass die Datei `MediaSDK.jar` ausgewählt ist.


1. Importieren Sie die Bibliothek.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

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

1. Implement the `MediaHeartbeatDelegate` interface.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Diese Instanz wird für alle der folgenden-Tracking-Ereignisse verwendet.

**App-Berechtigungen hinzufügen**

Ihre App, die das Medien-SDK verwendet, benötigt die folgenden Berechtigungen, um Daten in Tracking-Aufrufen zu senden:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Ergänzen Sie die Datei `AndroidManifest.xml` im Projektverzeichnis der Anwendung um die folgenden Zeilen, um diese Berechtigungen hinzuzufügen:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migration von Version 1.x auf 2.x in Android**

In den Versionen 2.x sind alle öffentlichen Methoden in der Klasse `com.adobe.primetime.va.simple.MediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern. Außerdem sind alle Konfigurationen nun in der `com.adobe.primetime.va.simple.MediaHeartbeatConfig`-Klasse konsolidiert.

For detailed information about migrating from 1.x to 2.x, see [mig-1x-2x-overview.md.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
