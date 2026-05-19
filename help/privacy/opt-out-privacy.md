---
title: Erklärung zu Opt-out und Datenschutz
description: Erfahren Sie, wie Sie Opt-in, Opt-out und Datenschutz handhaben können.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 382
ht-degree: 92%

---

# Opt-out und Datenschutz{#opt-out-and-privacy}

## Opt-out/Opt-in {#opt-out-opt-in}

Sie können steuern, ob das Nachverfolgen der Aktivitäten auf einem bestimmten Gerät zulässig ist:

* **Mobile Apps:** Die Medienerweiterungen berücksichtigen die Datenschutzeinstellungen in der Datenerfassung. Um das Tracking zu deaktivieren, müssen Sie die Datenschutzeinstellungen auf [Abgewählt in Tags](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property) setzen oder den [Datenschutzstatus in Mobile SDK aktualisieren](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#getprivacystatus).
* **JavaScript/Browser-Apps:** Die VA-Bibliothek respektiert die Datenschutz- und Optout-Einstellungen der `VisitorAPI`. Um das-Tracking zu deaktivieren, müssen Sie über den Besucher-API-Dienst die entsprechende Einstellung vornehmen. Weitere Informationen zum Opt-out und zum Datenschutz finden Sie unter [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).
* **OTT-Apps (Chromecast, Roku):** Die OTT-SDKs bieten APIs, die mit der Datenschutz-Grundverordnung (DSGVO) konform sind und es Ihnen ermöglichen, `opt`-Statuskennzeichen für die Datenerfassung und -übertragung zu setzen und lokal gespeicherte Identitäten abzurufen.

  >[!NOTE]
  >
  >Media Heartbeat-Tracking-Aufrufe werden ebenfalls deaktiviert, wenn der Datenschutzstatus auf „Opt-out“ festgelegt ist.

  Sie können wie folgt steuern, ob Analytics-Daten vom jeweiligen Gerät gesendet werden:

   * über die `privacyDefault`-Einstellung in der Konfigurationsdatei `ADBMobile.json`. Dies steuert die Grundeinstellung und bleibt bestehen, bis es im Code geändert wird.

   * Die `ADBMobile().setPrivacyStatus()`-Methode.

      * **Deaktivieren:**

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
        >Wenn ein Benutzer das Tracking deaktiviert, werden alle vorhandenen Gerätedaten und -IDs gelöscht, bis das Tracking erneut aktiviert wird.

      * **Wieder aktivieren:**

         * **Chromecast:**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
           ```

         * **Roku:**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
           ```

      * **Die aktuelle Einstellung zurückgeben:**

         * **Chromecast:**

           ```
           ADBMobile.config.getPrivacyStatus()
           ```

         * **Roku:**

           ```
           ADBMobile().getPrivacyStatus()
           ```

  Nachdem die Datenschutzeinstellung mithilfe von `setPrivacyStatus` geändert wurde, ist die Änderung dauerhaft, bis sie mit dieser Methode erneut geändert wird, es sei denn, die App wird deinstalliert und neu installiert.

## Abrufen von gespeicherten Kennungen (OTT-Apps) {#retrieving-stored-identifiers-ott-apps}

Mit diesen Informationen können Sie lokal gespeicherte Anwenderidentitäten von Ihrer Roku-Anwendung abrufen.

>[!IMPORTANT]
>
>Die Methode zum Abrufen aller Kennungen ruft alle dem SDK bekannten und beibehaltenen Benutzeridentitäten ab. Sie müssen diese Methode aufrufen, **bevor** sich ein Benutzer abmeldet.

Die lokal gespeicherten Identitäten werden in einer JSON-Zeichenfolge zurückgegeben, die Folgendes enthalten kann:

* Firmeninformationen: IMS-Org-IDs
* Benutzer-IDs
* Experience Cloud ID (MCID)
* Datenquellen-IDs (DPID, DPUUID)
* Analytics-IDs (AVID, AID, VID und zugehörige RSIDs)
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
