---
title: Zugriff auf Links zum Herunterladen von Media Analytics-SDKs
description: Links zu SDK-Downloads für die verfügbaren Plattformen, einschließlich Android, iOS, JavaScript, Chromecast und Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 81%

---

# Abrufen von Medien-SDKs, Erweiterungen mithilfe von Tags und OTT-SDKs {#download-sdks}

Die Informationen auf dieser Seite enthalten Links zum Herunterladen der aktuellen Medien-SDKs und zum Abrufen der Medienerweiterungen, die Tags verwenden.

Tags in Adobe Experience Platform sind die nächste Generation von Adobe-Verwaltungsfunktionen für Website-Tags und Mobile-SDKs. Tags bieten Kunden eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbelösungen bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse notwendig sind. Weitere Informationen zu Tags finden Sie in [Übersicht über Tags](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=de).


>[!NOTE]
>
>Informationen zum Herunterladen von veralteten SDKs finden Sie unter [Veraltet − SDKs herunterladen](/help/legacy/legacy-download-sdks.md).<br>
>>Wichtige Informationen zum Ende der Unterstützung finden Sie in den [häufig gestellten Fragen zum Ende der Unterstützung](/help/additional-resources/end-of-support-faqs.md).

## Medien-SDKs und Mobile-Bibliotheken {#media-sdks-libraries}

### Web-Implementierung {#download-web-sdk}

| Unterstützte Plattform | Unterstützte Lösungen | Implementierungsmethode | Version  |  APIs   |  Dokumentation  |  Beispiel  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript-Symbol ](assets/javascript-icon.png)</br>**JavaScript-API** | Adobe Analytics | Nur Analytics | Web − [Medien-SDK für JavaScript v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Referenz zur JavaScript-API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Installieren von Media SDK mithilfe von JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Beispiel des Medien-SDK für JavaScript v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript-Symbol ](assets/javascript-icon.png)</br>**JavaScript-API** | Adobe Analytics | Nur Analytics | Web − Medienerweiterung |  | [Erweiterung von Adobe Media Analytics (3.x SDK) für Audio und Video − Verwendung von Tags (Datenerfassung)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=de) | [Erweiterung von Adobe Media Analytics (3.x SDK) für Audio und Video – Beispiel](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [Implementieren der Streaming-Mediensammlung mit der Edge Network](/help/implementation/edge/implementation-edge.md) <p>und</p><p>[Senden von Web-Daten an Edge mit Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Mobile-Implementierung {#get-mobile-extension}

| Unterstützte Plattform | Unterstützte Lösungen | Implementierungsmethode | Version  |  Dokumentation   |  Beispieoe  |
|:---:|---|---|---|---|---|
| ![Android-Symbol ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Nur Analytics | Android − Medienerweiterung | [Mobile-SDKs – Dokumentation](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics – Media Analytics für Audio und Video – Beispiel](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS-Symbol ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Nur Analytics | iOS/tvOS − Medienerweiterung | [Mobile-SDKs – Dokumentation](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics – Media Analytics für Audio und Video – Beispiel](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Android-Symbol ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android – Experience Platform Edge | [Installieren von Media SDK mithilfe von JavaScript](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS-Symbol ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS – Experience Platform Edge | [Installieren von Media SDK mithilfe von JavaScript](/help/implementation/edge/implementation-edge.md) |  |

### Over-The-Top-Implementierung {#download-ott-libraries}

| Unterstützte Plattform | Unterstützte Lösungen | Implementierungsmethode | Version  |  APIs   |  Dokumentation  |
|:---:|---|---|---|---|---|
| ![Chromecast icon ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Nur Analytics | [SDK für Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast-API-Referenz](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Einrichten des Mobile SDK v3.x für Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku-Symbol ](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Nur Analytics | [SDK für Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Einrichten des Mobile SDK v2.x für Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Roku-Symbol ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Installieren von Media SDK mithilfe von JavaScript](/help/implementation/edge/implementation-edge.md) |
