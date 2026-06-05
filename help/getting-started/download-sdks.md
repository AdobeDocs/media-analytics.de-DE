---
title: Abrufen von Media SDKs, Erweiterungen und APIs
description: Links zu SDK-Downloads für die verfügbaren Plattformen, einschließlich Android, iOS, JavaScript, Chromecast und Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 575
ht-degree: 32%

---

# Abrufen von Media SDKs, Erweiterungen und APIs

## Edge-Implementierungen (empfohlen) {#edge-sdks}

Edge-Implementierungen erfassen Daten einmal und stellen sie über Adobe Experience Platform Edge Network an mehrere Ziele bereit: Adobe Analytics, Customer Journey Analytics, Adobe Journey Optimizer und Real-Time CDP. Verwenden Sie für Plattformen ohne native SDK (z. B. Smart-TVs, Spielekonsolen und Set-Top-Boxen) die Media Edge-API.

| | Dokumentation | Beispiel |
|:---:|---|---|
| [![JavaScript-Symbol](assets/javascript-icon.png)](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/install/overview)<br>[Web-SDK](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/install/overview) | [Einrichten der Web-SDK für Streaming-Medien](/help/implementation/edge/web-sdk.md) | [Beispiel](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![Erweiterungssymbol](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html)<br>[Web SDK-Tag-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html) | [Einrichten der Tag-Erweiterung „Web SDK&quot; für Streaming-Medien](/help/implementation/edge/web-sdk-tags.md) | [Beispiel](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Android-Symbol](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [Einrichten von Android für Streaming-Medien](/help/implementation/edge/android.md) | [Beispiel](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Apple iOS-Symbol](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [Einrichten von iOS für Streaming-Medien](/help/implementation/edge/ios.md) | [Beispiel](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![Erweiterungssymbol](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Android-Tag-Erweiterung](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Einrichten der Tag-Erweiterung &quot;Android&quot; für Streaming-Medien](/help/implementation/edge/android-tags.md) | |
| [![Erweiterungssymbol](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Tag-Erweiterung für iOS/tvOS](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Einrichten der Tag-Erweiterung &quot;iOS&quot; für Streaming-Medien](/help/implementation/edge/ios-tags.md) | |
| [![Roku icon](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[Roku SDK](https://github.com/adobe/aepsdk-roku) | [Roku für Streaming-Medien einrichten](/help/implementation/edge/roku.md) | [Beispiel](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![API-Symbol](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[Media Edge API](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [Einrichten der Media Edge-API](/help/implementation/edge/media-edge-api.md) | [Beispiel](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## Nur Analytics-Implementierungen {#analytics-only-sdks}

Diese SDKs und Erweiterungen senden Daten direkt an Adobe Analytics. Verwenden Sie für neue Implementierungen die oben genannten Edge-Implementierungen. Um vorhandene Analytics-Daten in Customer Journey Analytics oder andere Experience Platform-Programme zu importieren, verwenden Sie den [Analytics-Quell-Connector](https://experienceleague.adobe.com/de/docs/experience-platform/sources/connectors/adobe-applications/analytics).

| | Dokumentation | Beispiel |
|:---:|---|---|
| [![JavaScript icon](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Einrichten von JavaScript für Streaming-Medien](/help/implementation/analytics-only/javascript.md) | [Beispiel](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![Erweiterungssymbol](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=de)<br>[Medienerweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=de) | [Richten Sie JavaScript mithilfe von Tags für Streaming-Medien ein](/help/implementation/analytics-only/javascript-tags.md) | [Beispiel](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Chromecast icon](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Einrichten von Chromecast für Streaming-Medien](/help/implementation/analytics-only/chromecast.md) | [Beispiel](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![API-Symbol](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[Media Collection API](/help/implementation/media-collection-api/mc-api-overview.md) | [Einrichten der Media Collection-API](/help/implementation/analytics-only/media-collection-api.md) | |
