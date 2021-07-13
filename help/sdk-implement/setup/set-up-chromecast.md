---
title: Einrichten der Medien-SDK für Chromecast
description: Führen Sie diese Schritte aus, um die Media SDK-Anwendung in Chromecast einzurichten.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 96%

---

# Einrichten von Chromecast{#set-up-chromecast}

## FAQs

_Sollte ich das Chromecast JavaScript SDK verwenden oder kann ich das standardmäßige JavaScript SDK verwenden?_

Die richtige Antwort lautet „Chromecast“, und zwar aus den folgenden Gründen:
* Die AppMeasurement- und VisitorAPI-Bibliotheken im Standard-JS-SDK sind nicht für die Verwendung auf OTT-Plattformen zertifiziert. Im Chromecast JS SDK sind die Video Heartbeats Library (VHL), Analytics und VisitorAPI im einheitlichen, für Chromecast zertifizierten SDK integriert.
* Das Chromecast SDK ist wesentlich weniger umfangreich als das standardmäßige JS SDK. Dies ist für die von OTT-Plattformen verwendete kostengünstige Hardware von entscheidender Bedeutung.

## Voraussetzungen 

* **Gültige Konfigurationsparameter für Heartbeats festlegen:** Diese Parameter erhalten Sie nach der Einrichtung Ihres Media Analytics-Kontos von einem Adobe-Support-Mitarbeiter.
* **Stellen Sie die folgenden Funktionen in Ihrem Medienplayer bereit:**
   * *Eine API zum Abonnieren von Player-Ereignissen*: Das Media SDK erfordert den Aufruf einer Reihe einfacher APIs, wenn im Player Ereignisse auftreten.
   * *Eine API, die Player-Informationen bereitstellt*: Diese Informationen enthalten Details wie den Mediennamen und die Abspielposition.

Adobe Mobile Services bietet eine neue Anwenderoberfläche, auf der mobile Marketingfunktionen für mobile Anwendungen aus der gesamten Adobe Experience Cloud kombiniert werden. Zunächst bietet der Mobile Service eine nahtlose Integration von App-Analyse- und Targeting-Funktionen für die Lösungen Adobe Analytics und Adobe Target. Weitere Informationen finden Sie in der [Dokumentation zu Adobe Mobile Services.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=de)

Mit Chromecast-SDK 2.x für Experience Cloud-Lösungen können Sie in JavaScript geschriebene Chromecast-Anwendungen messen, Zielgruppendaten über das Zielgruppen-Management nutzen und erfassen und Videointeraktionen über Video-Heartbeats messen.

## SDK-Implementierung

1. Fügen Sie Ihre [heruntergeladene](/help/sdk-implement/download-sdks.md#download-2x-sdks) Chromecast-Bibliothek zu Ihrem Projekt hinzu.

   1. Die Datei `AdobeMobileLibrary-Chromecast-[version]` zip enthält folgende Softwarekomponenten:

      * `adbmobile-chromecast.min.js`:

         Diese Bibliothek ist im Quellordner Ihrer Chromecast-App enthalten.

      * `ADBMobileConfig`-Konfigurationsdatei

         Hierbei handelt es sich um die SDK-Konfigurationsdatei, die für Ihre App angepasst wird. Eine exemplarische `ADBMobileConfig`-Implementierung wird mit dem SDK mitgeliefert (unter `samples/`). Die richtigen Einstellungen erhalten Sie von einem Adobe-Support-Mitarbeiter.
   1. Fügen Sie die Bibliotheksdatei zu Ihrer `index.html`-Datei hinzu und erstellen Sie die globale Variable der `ADBMobileConfig` wie folgt (die globale Variable, mit der Adobe Mobile for Heartbeats konfiguriert wird, hat einen exklusiven Schlüssel namens `mediaHeartbeat`):

      ```js
      <script>
          var ADBMobileConfig = {
            "marketingCloud": {
              "org": "972C898555E9F7BC7F000101@AdobeOrg"
            },
            "target": {
              "clientCode": "",
              "timeout": 5
            },
            "audienceManager": {
              "server": "obumobile5.demdex.net"
            },
            "analytics": {
              "rsids": "mobile5vhl.sample.player",
              "server": "obumobile5.sc.omtrdc.net",
              "ssl": true,
              "offlineEnabled": false,
              "charset": "UTF-8",
              "lifecycleTimeout": 300,
              "privacyDefault": "optedin",
              "batchLimit": 0,
              "timezone": "MDT",
              "timezoneOffset": -360,
              "referrerTimeout": 0,
              "poi": []
            },
            "mediaHeartbeat": {
              "server": "obumobile5.hb.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
              "ovp": "chromecast-player",
              "sdkVersion": "chromecast-sdk",
              "playerName": "Chromecast"
            }
          };
        </script>
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >Wenn `mediaHeartbeat` nicht richtig konfiguriert ist, wechselt das Medienmodul (VHL) zu einem Fehlerstatus und sendet keine Tracking-Aufrufe mehr.

      ADBMobile-Konfigurationsparameter für mediaHeartbeat-Schlüssel:
   | Konfigurationsparameter | Beschreibung     |
   | --- | --- |
   | `server` | Zeichenfolge, die die URL des Tracking-Endpunkts am Backend angibt. |
   | `publisher` | Zeichenfolge, die den Publisher des Inhalts eindeutig identifiziert. |
   | `channel` | Zeichenfolge, die den Namen des Verbreitungskanals angibt. |
   | `ssl` | Boolescher Wert, der angibt, ob für Tracking-Aufrufe SSL verwendet werden soll. |
   | `ovp` | Zeichenfolge, die den Namen des Videoplayer-Anbieters angibt. |
   | `sdkversion` | Zeichenfolge, die die Version der Anwendung/des SDK angibt. |
   | `playerName` | Zeichenfolge, die den Namen des Players angibt. |


1. Konfigurieren der Experience Cloud-Besucher-ID.

   Der Besucher-ID-Dienst für Experience Platform stellt eine universale Besucher-ID für alle Experience Cloud-Lösungen bereit. Der Besucher-ID-Dienst ist für Video Heartbeat und andere Experience Cloud-Integrationen erforderlich.

   Stellen Sie sicher, dass Ihre `ADBMobileConfig`-Konfiguration Ihre `marketingCloud`-Organisations-ID enthält.

   ```js
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

   | Methode | Beschreibung |
   | --- | --- |
   | `getMarketingCloudID()` | Ruft die Experience Cloud-Besucher-ID vom Besucher-ID-Dienst ab.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Mit der Experience Cloud-Besucher-ID können Sie zusätzliche Kunden-IDs festlegen, die jedem Besucher zugeordnet werden können. Die Besucher-API akzeptiert mehrere Kunden-IDs für denselben Besucher sowie eine Kundentypkennung, die den Umfang der einzelnen Kunden-IDs abgrenzt. Diese Methode entspricht `setCustomerIDs()` in der JavaScript-Bibliothek.  Beispiel: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |



<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
