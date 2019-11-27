---
title: Roku einrichten
description: Einrichten der Media SDK-Anwendung für die Implementierung in Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Roku einrichten {#set-up-roku}

## Voraussetzungen

* **Gültige Konfigurationsparameter für Heartbeats festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Media Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **Stellen Sie in Ihrem Medienplayer folgende Funktionen bereit:**
   * _Eine API, um Player-Ereignisse zu abonnieren:_ Die Medien-SDK erfordert, dass Sie einige einfache APIs aufrufen, wenn Ereignisse in Ihrem Player auftreten.
   * _Eine API, die Playerinformationen bereitstellt:_ Diese Informationen enthalten Details wie z. B. Medienname und Abspielposition.

Adobe Mobile Services bietet eine neue Anwenderoberfläche, auf der mobile Marketingfunktionen für mobile Anwendungen aus der gesamten Adobe Experience Cloud kombiniert werden. Mobile Services ermöglicht die nahtlose Integration der App-Analyse- und Targeting-Funktionen der Adobe Analytics- und Adobe Target-Lösungen.

Weitere Informationen finden Sie in der [Dokumentation zu Adobe Mobile Services.](https://marketing.adobe.com/resources/help/de_DE/mobile/)

Mit Roku-SDK 2.x für Experience Cloud-Lösungen können Sie in BrightScript geschriebene Roku-Anwendungen messen, Zielgruppendaten über das Zielgruppen-Management nutzen und erfassen und Videointeraktionen über Video-Heartbeats messen.

## SDK-Implementierung

1. Fügen Sie Ihre [heruntergeladene](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku-Bibliothek zu Ihrem Projekt hinzu.

   1. Die Datei `AdobeMobileLibrary-2.*-Roku.zip` enthält folgende Softwarekomponenten:

      * `adbmobile.brs`: Diese Bibliothek ist im Quellordner Ihrer Roku-App enthalten.

      * `ADBMobileConfig.json`: Hierbei handelt es sich um die SDK-Konfigurationsdatei, die für Ihre App angepasst wird.
   1. Fügen Sie die Bibliotheks- und die JSON-Konfigurationsdatei zu Ihrer Projektquelle hinzu.

      Die JSON-Datei, die für die Konfiguration von Adobe Mobile verwendet wird, enthält einen exklusiven Schlüssel für Medien-Heartbeats namens `mediaHeartbeat`. Hier müssen Sie die Konfigurationsparameter für die Medien-Heartbeats hinzufügen.

      >[!TIP]
      >
      >Das Paket enthält eine `ADBMobileConfig`-JSON-Beispieldatei. Wenden Sie sich für die Einstellungen an Ihren Adobe-Support-Mitarbeiter.

      Beispiel:

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
          "offlineEnabled":false, 
          "lifecycleTimeout":30, 
          "batchLimit":50, 
          "privacyDefault":"optedin", 
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{ 
        "clientCode":"", 
        "timeout":5
      },
      "audienceManager":{ 
        "server":""
      },
      "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{ 
         "server":"example.com", 
         "publisher":"sample-publisher", 
         "channel":"sample-channel", 
         "ssl":false,
         "ovp":"sample-ovp", 
         "sdkVersion":"sample-sdk", 
         "playerName":"roku"
         }    
      }
      ```

      | Konfigurationsparameter | Beschreibung     |
      | --- | --- |
      | `server` | Zeichenfolge, die die URL des Tracking-Endpunkts am Backend angibt. |
      | `publisher` | Zeichenfolge, die den Publisher des Inhalts eindeutig identifiziert. |
      | `channel` | Zeichenfolge, die den Namen des Verbreitungskanals angibt. |
      | `ssl` | Boolescher Wert, der angibt, ob für Tracking-Aufrufe SSL verwendet werden soll. |
      | `ovp` | Zeichenfolge, die den Namen des Videoplayer-Anbieters angibt. |
      | `sdkversion` | Zeichenfolge, die die Version der Anwendung/des SDK angibt. |
      | `playerName` | Zeichenfolge, die den Namen des Players angibt. |

      >[!IMPORTANT]
      >
      >Wenn `mediaHeartbeat` nicht richtig konfiguriert ist, wechselt das Medienmodul (VHL) zu einem Fehlerstatus und sendet keine Tracking-Aufrufe mehr.


1. Konfigurieren der Experience Cloud-Besucher-ID.

   Der Experience Cloud-Besucher-ID-Dienst stellt eine universale Besucher-ID für alle Experience Cloud-Lösungen bereit. Der Besucher-ID-Dienst ist für Video Heartbeat- und andere Experience Cloud-Integrationen erforderlich.

   Stellen Sie sicher, dass Ihre `ADBMobileConfig`-Konfiguration Ihre `marketingCloud`-Organisations-ID enthält.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud-Organisations-IDs identifizieren eindeutig jedes Client-Unternehmen in Adobe Experience Cloud. Sie ähneln dem folgenden Wert: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass Sie `@AdobeOrg` angeben.

   Nach Abschluss der Konfiguration wird eine Experience Cloud-Besucher-ID generiert und allen Hits hinzugefügt. Andere Besucher-IDs wie `custom` und `automatically-generated` werden weiterhin mit den Treffern gesendet.

   **Methoden des Experience Cloud-Besucher-ID-Dienstes**

   >[!TIP]
   >
   >Experience Cloud-Besucher-ID-Methoden wird `visitor` vorangestellt.

   |  Methode   | Beschreibung |
   | --- | --- |
   | `visitorMarketingCloudID` | Ruft die Experience Cloud-Besucher-ID vom Besucher-ID-Dienst ab.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Mit der Experience Cloud-Besucher-ID können Sie zusätzliche Kunden-IDs festlegen, die jedem Besucher zugeordnet werden können. Die Besucher-API akzeptiert mehrere Kunden-IDs für denselben Besucher sowie eine Kundentypkennung, die den Umfang der einzelnen Kunden-IDs abgrenzt. Diese Methode entspricht `setCustomerIDs`. Beispiel: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Wird verwendet, um die Roku-ID für Werbung (RIDA) im SDK festzulegen. Beispiel: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Rufen Sie die Roku-ID für Werbung (RIDA) mit der [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic)-API des Roku-SDK ab. |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->
