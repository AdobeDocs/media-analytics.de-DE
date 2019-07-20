---
seo-title: Opt-out und Datenschutz
title: Opt-out und Datenschutz
uuid: 7 e 60 c 7 bd -8 dba -4 c 7 a -9 c 3 c -0 c 634 b 815397
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# Opt-out und Datenschutz{#opt-out-and-privacy}

## Opt-out/Opt-in {#section_zfb_syq_v2b}

Sie können steuern, ob die Tracking-Aktivität auf einem bestimmten Gerät zulässig ist:

* **Mobile Apps:** Die VA-Bibliothek respektiert die Datenschutz- und Opt-out-Einstellungen der `AdobeMobile`-Bibliothek. Zum Abmelden vom Tracking müssen Sie die `AdobeMobile`-Bibliothek verwenden. Weitere Informationen zu den Opt-out- und Datenschutzeinstellungen der `AdobeMobile`-Bibliothek finden Sie unter [Opt-out- und Datenschutzeinstellungen](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html).
* **JavaScript/Browser-Apps:** Die VA-Bibliothek respektiert die Datenschutz- und Optout-Einstellungen der `VisitorAPI`. Um das-Tracking zu deaktivieren, müssen Sie über den Besucher-API-Dienst die entsprechende Einstellung vornehmen. For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **OTT-Apps (Chromecast, Roku) -** Die OTT sdks stellen allgemeine GDPR (Data Protection Protection)-apis bereit, mit denen `opt` Sie Statusflags für die Datenerfassung und -übertragung festlegen und lokal gespeicherte Identitäten abrufen können.

   >[!NOTE]
   >
   >Media Heartbeat-Verfolgungsaufrufe sind ebenfalls deaktiviert, wenn der Datenschutzstatus auf "Opt-out" eingestellt ist.

   Sie können wie folgt steuern, ob Analytics-Daten vom jeweiligen Gerät gesendet werden:

   * `privacyDefault` Die Einstellung in der `ADBMobile.json` Konfigurationsdatei. Dies steuert die Grundeinstellung und bleibt bestehen, bis es im Code geändert wird.

   * The `ADBMobile().setPrivacyStatus()` method.

      * **Opt-out:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >Wenn ein Benutzer die Verfolgung ablehnt, werden alle Daten und IDs des beibehaltenen Geräts bereinigt, bis der Benutzer sich wieder anmeldet.

      * **Wiederanmeldung in:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Zurücksetzen der aktuellen Einstellung:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   Nachdem die Datenschutzeinstellung mit `setPrivacyStatus` geändert wurde, ist die Änderung dauerhaft, bis sie mit dieser Methode erneut geändert wird, es sei denn, die App wird deinstalliert und neu installiert.

## Abrufen von gespeicherten Kennungen (OTT-Apps) {#section_mky_2yq_v2b}

Mit diesen Informationen können Sie lokal gespeicherte Anwenderidentitäten von Ihrer Roku-Anwendung abrufen.

>[!IMPORTANT]
>
>Die Methode zum Abrufen aller Identifikatoren ruft alle bekannten Benutzer ab und bleibt vom SDK erhalten. Diese Methode muss **vor** einem Opt-out des Anwenders aufgerufen werden.

Die lokal gespeicherten Identitäten werden in einer JSON-Zeichenfolge zurückgegeben, die folgende Elemente enthalten kann:

* Unternehmenskontext – IMS-Org-ID
* Anwender-IDs
* Experience Cloud ID (MCID)
* Datenquellen-IDs (DPID, DPUUID)
* Analytics-IDs (AVID, AID, VID und verbundene RSIDs)
* Audience Manager-ID (UUID)

Beispiel:

* **Chromecast:**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku:**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

