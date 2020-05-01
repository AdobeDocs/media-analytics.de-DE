---
title: Android einrichten
description: Einrichten der Media SDK-Anwendung für die Implementierung in Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: be82be2eb58f89344f2125288599fef461db441e

---


# Android einrichten {#set-up-android}

>[!IMPORTANT]
>
>Ab Oktober 2020 beendet Adobe die Unterstützung für die SDKs der Version 4 Mobile und die eigenständigen Medienanalysen-SDKs für Android. Sie können die SDKs der Version 4 weiterhin herunterladen und verwenden, aber der Kundendienst und der Zugriff auf Foren werden eingestellt. Sie sollten zu den Adobe Experience Platform (AEP) SDKs für Android migrieren. Das AEP Mobile SDK (früher als v5 bezeichnet) unterstützt ausschließlich Adobe Experience Cloud-Funktionen. Weitere Informationen zu dieser Änderung finden Sie unter Häufig gestellte Fragen zum Ende der Unterstützung für [Version 4 Mobile SDKs](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq). Es wird empfohlen, zum neuen AEP Mobile SDK zu migrieren.
Nach der Migration zum AEP Mobile SDK müssen Sie die Analytics-Startererweiterung und die Media Analytics-Startererweiterung implementieren, um Adobe Analytics für Audio und Video zu aktivieren. Weitere Informationen zur Migration auf das neue AEP Mobile SDK finden Sie unter [Migration vom eigenständigen Media SDK zum Adobe Launch ](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)


## Voraussetzungen


* **Gültige Konfigurationsparameter für Media SDK festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **ADBMobile für Android in Ihre Anwendung implementieren:** Weitere Informationen zur Adobe Mobile-SDK-Dokumentation finden Sie unter [Android-SDK 4.x für Experience Cloud-Lösungen.](https://docs.adobe.com/content/help/de-DE/mobile-services/android/overview.html)

* **Stellen Sie die folgenden Funktionen in Ihrem Medienplayer bereit:**
   * *Eine API zum Abonnieren von Player-Ereignissen*: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * *Eine API, die Player-Informationen bereitstellt*: Diese Informationen enthalten Details wie den Mediennamen und die Abspielposition.

## SDK-Implementierung

1. Fügen Sie Ihr [heruntergeladenes](/help/sdk-implement/download-sdks.md#download-2x-sdks) Medien-SDK zu Ihrem Projekt hinzu.

   1. Erweitern Sie die Android-Zip-Datei (z. B. `MediaSDK-android-v2.*.zip`).
   1. Stellen Sie sicher, dass die Datei `MediaSDK.jar` im Verzeichnis `libs/` vorhanden ist.

   1. Fügen Sie die Bibliothek zu Ihrem Projekt hinzu.

      **IntelliJ IDEA:**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. Auswählen **[!UICONTROL Open Module Settings]**.
      1. Wählen Sie **[!UICONTROL Project Settings]** unter **[!UICONTROL Libraries]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Wählen Sie **[!UICONTROL Java]** und navigieren Sie zur Datei `MediaSDK.jar`.

      1. Wählen Sie die Module aus, in denen Sie die Mobile-Bibliothek verwenden möchten.
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse:**

      1. Klicken Sie in der Eclipse IDE mit der rechten Maustaste auf den Projektnamen.
      1. Klicken Sie auf  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Auswählen `MediaSDK.jar`.
      1. Klicken Sie auf **[!UICONTROL Open]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Klicken Sie auf die **[!UICONTROL Order]** und **[!UICONTROL Export]** Registerkarten.

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

Weitere Informationen zur Migration von 1.x zu 2.x finden Sie unter [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
