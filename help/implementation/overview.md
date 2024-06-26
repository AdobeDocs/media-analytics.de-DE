---
title: Implementieren des Streaming Media Collection Add-ons
description: Erfahren Sie mehr über die Implementierungspfade für das Streaming Media Collection Add-on.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 69%

---

# Implementieren des Streaming Media Collection Add-ons

Es gibt verschiedene Möglichkeiten, das Adobe Streaming Media Collection Add-on zu implementieren. Einen detaillierten Vergleich der unterstützten Geräte und Plattformen für die auf dieser Seite beschriebenen Implementierungsmethoden finden Sie unter [Unterstützte Geräte und Plattformen](/help/getting-started/supported-devices.md).

## Edge-Implementierungsmethoden

Wir empfehlen die Verwendung von Edge bei der Implementierung des Streaming-Mediensammlungs-Add-ons für alle neuen Adobe Analytics- oder Customer Journey Analytics-Kunden.

* **Media for Edge Network SDK/Erweiterung:** Erfasst Daten von Web-, iOS- und Android-Geräten oder Roku-Geräten und sendet sie an Edge Network. Die Daten können dann entweder an Customer Journey Analytics oder Adobe Analytics gesendet werden.

  Weitere Informationen zur Media for Edge Network SDK/Erweiterung finden Sie unter [Implementieren des Add-ons für Streaming-Mediensammlung mit dem Edge Network](/help/implementation/edge/implementation-edge.md).

* **Media Edge-API:** Kann angepasst werden, um Daten von beliebigen Geräten oder Formaten (einschließlich Mobilgeräten, Web- und Over-the-Top-Geräten) zu erfassen und Daten an Edge Network zu senden. Die Daten können dann entweder an Customer Journey Analytics oder Adobe Analytics gesendet werden.

  Weitere Informationen zur Media Edge-API finden Sie unter [Übersicht über die Media Edge API](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![CJA-Workflow](assets/streaming-media-edge.png)

## Implementierungsmethoden nur für Adobe Analytics

Die oben beschriebenen Edge-Implementierungsmethoden werden sowohl für Customer Journey Analytics als auch für Adobe Analytics empfohlen, insbesondere für neue Implementierungen.

Zusätzlich zu den Edge-Implementierungsmethoden sind weitere Implementierungsmethoden verfügbar. Diese Implementierungsmethoden wurden für die Verwendung mit Adobe Analytics entwickelt. Bestehende Kundinnen und Kunden mit einer der folgenden Implementierungsmethoden können jedoch weiterhin Daten in Customer Journey Analytics zur Verfügung stellen, indem sie eine [Analytics-Quellverbindung](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=de) erstellen.

* **Media-Erweiterung mit Tags:** Die Erweiterung „Adobe Media Analytics für Audio und Video“ bietet die Funktionalität zum Hinzufügen der Media-Tracker-Instanz zu einer Site oder einem Projekt, für die bzw. das Tags aktiviert sind. Die Daten werden an Adobe Analytics gesendet.

  Informationen zum Installieren, Konfigurieren und Implementieren der Media-Erweiterung mit Tags finden Sie unter [Übersicht über die Erweiterung Adobe Media Analytics (3.x SDK) für Audio und Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html?lang=de).

* **Medien-SDK:** Mit dem Medien-SDK können Sie mehrere Medienplattformen messen, darunter Websites, Mobiltelefone, vernetzte TVs, Tablets, OTT-Geräte, Set-Top-Boxen und Spielekonsolen. (Weitere Informationen finden Sie unter [Unterstützte Geräte und Plattformen](/help/getting-started/supported-devices.md).)

  Die Medien-SDKs verwenden die Mediensammlungs-APIs für das Tracking. Die Daten werden an Adobe Analytics gesendet.

  Informationen zum Herunterladen und Installieren von Media-SDKs und Erweiterungen finden Sie unter [Abrufen von Media-SDKs, Erweiterungen mithilfe von Tags und OTT-SDKs](/help/getting-started/download-sdks.md).

* **Mediensammlungs-APIs:** Da die Mediensammlungs-APIs anpassbar sind, können sie für Anwendungen verwendet werden, die benutzerdefinierte Tracking-Funktionen erfordern, sowie für Geräte, die von den Medien-SDKs nicht unterstützt werden. Die Mediensammlungs-APIs verfolgen Audio- und Videoereignisse über RESTful HTTP-Aufrufe. Die Daten werden an Adobe Analytics gesendet.

  Informationen zur Verwendung der Mediensammlungs-APIs finden Sie unter [Mediensammlungs-APIs](media-collection-api/mc-api-overview.md).


![Analytics-Workflow](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
