---
title: Opt-out- und Datenschutzeinstellungen
description: Erfahren Sie, wie Sie Opt-in, Opt-out und Datenschutz handhaben können.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 8b9e7582923a61bd2a43049a02ce36727a677e17
workflow-type: tm+mt
source-wordcount: 798
ht-degree: 3%

---

# Opt-out- und Datenschutzeinstellungen

Wenn ein Benutzer das Tracking abwählt, stoppt die Streaming-Medienbibliothek sofort alle Datenerfassungsaktivitäten. Für diesen Benutzer werden keine Sitzungsstart-Aufrufe, keine Heartbeat-Pings und keine Ereignisverfolgungsdaten an die Datenerfassungs-Server von Adobe gesendet.

## Opt-out/Opt-in

Opt-out-Steuerelemente werden pro Gerät oder Browser ausgeführt. Für die Einhaltung der Benutzerzustimmung ist die implementierende Organisation verantwortlich. Einen Überblick über die Datenschutzpraktiken von Adobe finden Sie im [Adobe Privacy Center](https://www.adobe.com/de/privacy.html).

## Empfohlene Implementierungsarten

>[!BEGINTABS]

>[!TAB Web SDK]

Web SDK berücksichtigt die mit dem Befehl `setConsent` festgelegten Einverständnisvoreinstellungen. Wenn das Einverständnis auf `"out"` festgelegt ist, stoppt die Web-SDK die Weiterleitung aller Ereignisse, einschließlich Streaming-Medien-Tracking-Aufrufen, an die Edge Network. Der Einverständnisstatus bleibt zwischen Sitzungen im Browser-Speicher erhalten.

Stellen Sie vor der Implementierung des Opt-outs sicher, dass Ihre Web-SDK mit der Streaming-Medienkomponente konfiguriert ist. Weitere Informationen finden Sie unter [Einrichten von Web SDK](../implementation/edge/web-sdk.md).

Legen Sie das Einverständnis für das Opt-out mit dem Einverständnisstandard für Adobe 2.0 fest:

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

Einverständniswerte:

* `"y"`: Opt-in (Datenerfassung zulässig)
* `"n"`: Opt-out (Datenerfassung unterdrückt)
* `"p"`: Ausstehend (wartet auf Benutzerentscheidung; bis zur Lösung werden keine Daten erfasst)

Um das Tracking wiederherzustellen, rufen Sie `setConsent` erneut mit `"y"` als `collect.val` auf.

Weitere Informationen [ anderen Formaten, einschließlich IAB TCF 2.0, finden Sie ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/setconsent) Befehl „setConsent“ in der Web SDK-Dokumentation.

>[!TAB iOS]

Adobe Experience Platform Mobile SDK respektiert den Datenschutzstatus, der mithilfe von `MobileCore.setPrivacyStatus()` festgelegt wurde. Wenn Sie den Status auf `.optedOut` setzen, wird die gesamte Datenerfassung über alle AEP-Erweiterungen hinweg unterdrückt, einschließlich Streaming Media. Der Status bleibt in allen App-Sitzungen bestehen.

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

Um das Tracking wiederherzustellen, setzen Sie den Datenschutzstatus wieder auf `.optedIn`:

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

Weitere Informationen finden Sie unter [Datenschutz und DSGVO](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) in der Dokumentation zu AEP Mobile SDK.

>[!TAB Android]

Adobe Experience Platform Mobile SDK respektiert den Datenschutzstatus, der mithilfe von `MobileCore.setPrivacyStatus()` festgelegt wurde. Wenn Sie den Status auf `MobilePrivacyStatus.OPT_OUT` setzen, wird die gesamte Datenerfassung über alle AEP-Erweiterungen hinweg unterdrückt, einschließlich Streaming Media. Der Status bleibt in allen App-Sitzungen bestehen.

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

Um das Tracking wiederherzustellen, setzen Sie den Datenschutzstatus wieder auf `MobilePrivacyStatus.OPT_IN`:

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

Weitere Informationen finden Sie unter [Datenschutz und DSGVO](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) in der Dokumentation zu AEP Mobile SDK.

>[!TAB Roku Edge]

Roku Edge SDK verwendet `setConsent()` mit dem Einverständnisstandard Adobe 2.0. Wenn Sie `collect.val` auf `"n"` setzen, wird die Erfassung aller Daten, einschließlich Streaming-Medienereignissen, sofort gestoppt.

Einverständniswerte:

* `"y"`: Opt-in (Datenerfassung zulässig)
* `"n"`: Opt-out (Datenerfassung unterdrückt)
* `"p"`: Ausstehend (wartet auf Benutzerentscheidung; bis zur Lösung werden keine Daten erfasst)

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

Um das Tracking wiederherzustellen, setzen Sie `collect.val` auf `"y"` und rufen Sie `setConsent()` erneut auf.

Sie können bei der SDK-Initialisierung auch einen standardmäßigen Einverständniswert festlegen, indem Sie `updateConfiguration()` mit dem `ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT` Schlüssel verwenden. Weitere Informationen finden Sie in der [Dokumentation zu Edge SDK](https://github.com/adobe/aepsdk-roku).

>[!TAB Media Edge-API]

Die Media Edge-API ist eine Server-seitige Implementierung. Keine SDK-Ebene erzwingt automatisch das Einverständnis - Ihr Programm muss den Einverständnisstatus des Benutzers überprüfen, bevor API-Aufrufe durchgeführt werden, und Anfragen für abgemeldete Benutzer unterdrücken.

Für eine vollständige Abmeldung führen Sie für Benutzer, die sich per Opt-out abgemeldet haben, keine POST an den `/va/v2/sessions`-Endpunkt (oder alle nachfolgenden Ereignis-Endpunkte) durch:

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

Weitere Informationen finden Sie in der [Media Edge-API-Referenz](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

>[!ENDTABS]

## Legacy-Implementierungstypen (nur Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Die Media SDK JS 3.x-Bibliothek bezieht sich auf den Opt-out-Status der Adobe-Besucher-API (Identity Service). Wenn Benutzende die Verwendung der Besucher-API abmelden, unterdrückt Media SDK automatisch alle Tracking-Aufrufe.

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

Ersetzen Sie `YOUR_ORG_ID@AdobeOrg` durch Ihre Organisations-ID aus Adobe Admin Console.

Um das Tracking wiederherzustellen, übergeben Sie `false` an `setOptOut()`.

Weitere Informationen finden Sie unter [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).

>[!TAB Chromecast]

Chromecast Media SDK 3.x respektiert den Datenschutzstatus, der mithilfe von `ADBMobile.config.setPrivacyStatus()` festgelegt wurde. Wenn Sie den Status auf `PRIVACY_STATUS_OPT_OUT` setzen, wird die gesamte Datenerfassung unterdrückt.

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

Um das Tracking wiederherzustellen, setzen Sie den Status zurück auf „Angemeldet“:

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

Sie können auch den Standarddatenschutzstatus bei der SDK-Initialisierung in Ihrem `ADBMobileConfig` festlegen:

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB Roku 2.x]

Roku 2.x SDK respektiert den Datenschutzstatus, der mithilfe von `setPrivacyStatus` festgelegt wurde. Wenn Sie den Status auf `PRIVACY_STATUS_OPT_OUT` setzen, wird die gesamte Datenerfassung unterdrückt.

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_OUT)
```

Um das Tracking wiederherzustellen, setzen Sie den Status zurück auf „Angemeldet“:

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_IN)
```

Sie können auch den standardmäßigen Datenschutzstatus bei der SDK-Initialisierung in Ihrer `ADBMobileConfig.json` festlegen:

```json
"analytics": {
  "privacyDefault": "optedout"
}
```

>[!TAB Media Collection API]

Die Mediensammlungs-API ist eine Server-seitige Implementierung. Ihre Anwendung muss den Benutzereinverständnisstatus überprüfen, bevor sie API-Aufrufe durchführt und Anfragen für abgemeldete Benutzer unterdrückt.

Für eine vollständige Abmeldung führen Sie für Benutzer, die sich per Opt-out abgemeldet haben, keine POST-Anfrage an den Sitzungs-Endpunkt durch.

Fügen Sie für partielle Opt-outs im Rahmen des CCPA Opt-out-Flags in das `params` Objekt Ihrer `sessionStart`-Anfrage ein:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`: Legen Sie die Einstellung auf `true` fest, um die Freigabe von Daten durch Adobe Analytics und andere Experience Cloud-Lösungen (wie Audience Manager) zu verhindern.
* `analytics.optOutShare`: Legen Sie die Einstellung auf `true` fest, um die gemeinsame Nutzung von Daten durch andere Adobe Analytics-Clients zu deaktivieren.

Eine vollständige Liste der verfügbaren Parameter finden Sie in der [Referenz zu Media Collection API-Anforderungsparametern](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md).

>[!ENDTABS]
