---
title: Android einrichten
description: Einrichten der Media SDK-Anwendung für die Implementierung in Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Android einrichten {#set-up-android}

## Voraussetzungen

* **Gültige Konfigurationsparameter für Media SDK festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **ADBMobile für Android in Ihre Anwendung implementieren:** Weitere Informationen zur Adobe Mobile-SDK-Dokumentation finden Sie unter [Android-SDK 4.x für Experience Cloud-Lösungen.](https://marketing.adobe.com/resources/help/de_DE/mobile/android/)
* **Stellen Sie in Ihrem Medienplayer folgende Funktionen bereit:**
   * *Eine API, um Player-Ereignisse zu abonnieren:* Die Medien-SDK erfordert, dass Sie einige einfache APIs aufrufen, wenn Ereignisse in Ihrem Player auftreten.
   * *Eine API, die Playerinformationen bereitstellt:* Diese Informationen enthalten Details wie z. B. Medienname und Abspielposition.

## SDK-Implementierung

1. Fügen Sie Ihr [heruntergeladenes](/help/sdk-implement/download-sdks.md#download-2x-sdks) Medien-SDK zu Ihrem Projekt hinzu.

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
      1. Klicken Sie auf **[!UICONTROL Pfad aufbauen]** &gt; **[!UICONTROL Externe Archive hinzufügen]** .
      1. Auswählen `MediaSDK.jar`.
      1. Klicken Sie auf **[!UICONTROL Öffnen]**.
      1. Klicken Sie erneut mit der rechten Maustaste auf das Projekt und klicken Sie dann auf  **[!UICONTROL Pfad aufbauen]** &gt; **[!UICONTROL Pfadaufbau konfigurieren]**.
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

**App-Berechtigungen hinzufügen**

Ihre App, die das Medien-SDK verwendet, benötigt die folgenden Berechtigungen, um Daten in Tracking-Aufrufen zu senden:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Ergänzen Sie die Datei `AndroidManifest.xml` im Projektverzeichnis der Anwendung um die folgenden Zeilen, um diese Berechtigungen hinzuzufügen:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migration von Version 1.x auf 2.x in Android**

In den Versionen 2.x sind alle öffentlichen Methoden in der Klasse `com.adobe.primetime.va.simple.MediaHeartbeat` konsolidiert, um die Arbeit der Entwickler zu erleichtern. Außerdem sind alle Konfigurationen nun in der `com.adobe.primetime.va.simple.MediaHeartbeatConfig`-Klasse konsolidiert.

Weitere Informationen zur Migration von 1.x zu 2.x finden Sie unter [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
