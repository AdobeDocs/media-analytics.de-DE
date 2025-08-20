---
title: Einrichten des Media SDK für Roku
description: Führen Sie diese Schritte aus, um das Media SDK-Programm in Roku einzurichten.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 92%

---

# Einrichten von Mobile SDK v2.x für Roku {#set-up-roku}

## Voraussetzungen  {#roku-prerequisites}

* **Abrufen gültiger Konfigurationsparameter für Adobe Streaming Media Services**

  Sie können diese Parameter von einem Adobe-Support-Mitarbeiter erhalten, nachdem Sie Ihr Konto für das Add-on &quot;Adobe Streaming Media Collection“ oder das Add-on „Adobe Analytics for Streaming Media“ eingerichtet haben.

* **Integrieren der folgenden APIs in Ihren Media Player**

   * _Eine API zum Abonnieren von Player-Ereignissen_: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * _Eine API, die Player-Informationen bereitstellt_: Diese Informationen enthalten Details wie den Mediennamen und die Abspielposition.

Mit Roku SDK 2.x für Experience Cloud-Lösungen können Sie in BrightScript geschriebene Roku-Anwendungen messen, Zielgruppendaten durch Zielgruppen-Management nutzen sowie erfassen und Videointeraktionen über Videoereignisse messen.

## Mobile Library-/SDK-Implementierung

1. Fügen Sie Ihre [heruntergeladene](/help/getting-started/download-sdks.md) Roku-Bibliothek zu Ihrem Projekt hinzu.

   1. Die Datei `AdobeMobileLibrary-2.*-Roku.zip` enthält folgende Softwarekomponenten:

      * `adbmobile.brs`: Diese Bibliothek ist im Quellordner Ihrer Roku-App enthalten.

      * `ADBMobileConfig.json`: Hierbei handelt es sich um die SDK-Konfigurationsdatei, die für Ihre App angepasst wird.

   1. Fügen Sie die Bibliotheks- und die JSON-Konfigurationsdatei zu Ihrer Projektquelle hinzu.

      Die JSON-Datei, die für die Konfiguration von Adobe Mobile verwendet wird, enthält einen exklusiven Schlüssel für Media Analytics namens `mediaHeartbeat`. Hier liegen die Konfigurationsparameter für Media Analytics an.

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
          "ssl":true,
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
         "ssl":true,
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

   Der Besucher-ID-Dienst für Experience Platform stellt eine universale Besucher-ID für alle Experience Cloud-Lösungen bereit. Der Besucher-ID-Dienst ist für Videoereignisse und andere Experience Cloud-Integrationen erforderlich.

   Stellen Sie sicher, dass Ihre `ADBMobileConfig`-Konfiguration Ihre `marketingCloud`-Organisations-ID enthält.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
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
   | `visitorMarketingCloudID` | Ruft die Experience Cloud-Besucher-ID aus dem Besucher-ID-Dienst ab.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Mit der Experience Cloud-Besucher-ID können Sie zusätzliche Kunden-IDs festlegen, die jedem Besucher zugeordnet werden können. Die Besucher-API akzeptiert mehrere Kunden-IDs für denselben Besucher sowie eine Kundentypkennung, die den Umfang der einzelnen Kunden-IDs abgrenzt. Diese Methode entspricht `setCustomerIDs`. Beispiel: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Wird verwendet, um die Roku-ID für Werbung (RIDA) im SDK festzulegen. Beispiel: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Rufen Sie die Roku-ID für Werbung (RIDA) mit der [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic)-API des Roku-SDK ab. |
   | `getAllIdentifiers` | Gibt eine Liste aller vom SDK gespeicherten Kennungen zurück, einschließlich Analytics-, Besucher-, Audience Manager- und benutzerdefinierter Kennungen. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |

   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **Zusätzliche öffentliche APIs**

   **DebugLogging**

   |  Methode   | Beschreibung |
   | --- | --- |
   | `setDebugLogging` | Wird zum Aktivieren oder Deaktivieren der Debugging-Protokollierung für das SDK verwendet. <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | Gibt „true“ zurück, wenn die Debugging-Protokollierung aktiviert ist. <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  Konstante  | Beschreibung |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | Konstante, die beim Aufruf von setPrivacyStatus zum Opt-in übergeben wird. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | Konstante, die beim Aufruf von setPrivacyStatus zum Opt-out übergeben wird. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  Methode   | Beschreibung |
   | --- | --- |
   | `setPrivacyStatus` | Legt den Datenschutzstatus im SDK fest. <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Ruft den aktuellen Datenschutzstatus ab, der im SDK festgelegt ist. <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >Rufen Sie alle 250 ms in der Hauptereignisschleife die Funktionen `processMessages` und `processMediaMessages` auf, damit das SDK die Pings ordnungsgemäß sendet.

   |  Methode   | Beschreibung |
   | --- | --- |
   | `processMessages` | Verantwortlich für die Übergabe der Analytics-Ereignisse an das SDK zur Verarbeitung.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Verantwortlich für die Übergabe der Medienereignisse an das SDK zur Verarbeitung. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html?lang=de) -->
