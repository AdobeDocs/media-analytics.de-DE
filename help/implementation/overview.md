---
title: Implementieren von Streaming-Mediendiensten für Adobe Analytics oder Customer Journey Analytics
description: Erfahren Sie mehr über die Implementierungspfade für Adobe Streaming Media Services.
uuid: null
feature: Streaming Media
role: User, Admin, Developer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
TQID: https://experienceleague.adobe.com/aFrxbzBLlf1ngetaM-GsNFXz6TUXi6Pic3quLVI297c
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 518
ht-degree: 66%

---

# Implementieren von Streaming-Mediendiensten für Adobe Analytics oder Customer Journey Analytics

Es gibt verschiedene Möglichkeiten, Adobe-Streaming-Mediendienste zu implementieren. Einen detaillierten Vergleich der unterstützten Geräte und Plattformen für die auf dieser Seite beschriebenen Implementierungsmethoden finden Sie unter [Unterstützte Geräte und Plattformen](/help/getting-started/supported-devices.md).

## Edge-Implementierungsmethoden

Adobe empfiehlt für alle neuen Adobe Analytics- oder Customer Journey Analytics-Kunden die Verwendung von Edge Network-Implementierungsmethoden.

* **Medien für Edge Network SDK/Erweiterung:** Sammelt Daten aus dem Web, iOS- und Android-Geräten oder Roku-Geräten und sendet sie an Edge Network. Die Daten können dann entweder an Customer Journey Analytics oder Adobe Analytics gesendet werden.

  Weitere Informationen zu Media for Edge Network SDK/Extension finden Sie in der [Edge-Implementierungsübersicht](/help/implementation/edge/overview.md).

* **Media Edge-API** Kann angepasst werden, um Daten von jedem Gerät oder Format (einschließlich Mobilgeräten, Web- und Over-the-top-Geräten) zu erfassen und Daten an Edge Network zu senden. Die Daten können dann entweder an Customer Journey Analytics oder Adobe Analytics gesendet werden.

  Weitere Informationen zur Media Edge-API finden Sie unter [Media Edge-API - Übersicht](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![CJA-Workflow](assets/streaming-media-edge.png)

## Implementierungsmethoden nur für Adobe Analytics

Die oben beschriebenen Edge-Implementierungsmethoden werden sowohl für Customer Journey Analytics als auch für Adobe Analytics empfohlen, insbesondere für neue Implementierungen.

Zusätzlich zu den Edge-Implementierungsmethoden sind weitere Implementierungsmethoden verfügbar. Diese Implementierungsmethoden wurden für die Verwendung mit Adobe Analytics entwickelt. Bestehende Kundinnen und Kunden mit einer der folgenden Implementierungsmethoden können jedoch weiterhin Daten in Customer Journey Analytics zur Verfügung stellen, indem sie eine [Analytics-Quellverbindung](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=de) erstellen.

Nur Adobe Analytics-Implementierungsmethoden verwenden das Add-on Adobe Analytics for Streaming Media . Voraussetzungen und eine Liste von Methoden finden Sie unter [Nur Analytics-Implementierung - Übersicht](/help/implementation/analytics-only/overview.md).

* **Media-Erweiterung mit Tags:** Die Erweiterung „Adobe Media Analytics für Audio und Video“ bietet die Funktionalität zum Hinzufügen der Media-Tracker-Instanz zu einer Site oder einem Projekt, für die bzw. das Tags aktiviert sind. Die Daten werden an Adobe Analytics gesendet.

  Informationen zum Installieren, Konfigurieren und Implementieren der Media-Erweiterung mit Tags finden Sie unter [Übersicht über die Erweiterung Adobe Media Analytics (3.x SDK) für Audio und Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html?lang=de).

* **Medien-SDK:** Mit dem Medien-SDK können Sie mehrere Medienplattformen messen, darunter Websites, Mobiltelefone, vernetzte TVs, Tablets, OTT-Geräte, Set-Top-Boxen und Spielekonsolen. (Weitere Informationen finden Sie unter [Unterstützte Geräte und Plattformen](/help/getting-started/supported-devices.md).)

  Die Medien-SDKs verwenden die Mediensammlungs-APIs für das Tracking. Die Daten werden an Adobe Analytics gesendet.

  Informationen zum Herunterladen und Installieren von Media-SDKs und Erweiterungen finden Sie unter [Abrufen von Media-SDKs, Erweiterungen mithilfe von Tags und OTT-SDKs](/help/getting-started/download-sdks.md).

* **Mediensammlungs-APIs:** Da die Mediensammlungs-APIs anpassbar sind, können sie für Anwendungen verwendet werden, die benutzerdefinierte Tracking-Funktionen erfordern, sowie für Geräte, die von den Medien-SDKs nicht unterstützt werden. Die Mediensammlungs-APIs verfolgen Audio- und Videoereignisse über RESTful HTTP-Aufrufe. Die Daten werden an Adobe Analytics gesendet.

  Informationen zur Verwendung der Mediensammlungs-APIs finden Sie unter [Mediensammlungs-APIs](media-collection-api/mc-api-overview.md).


![Analytics-Workflow](assets/analytics-implementation.png)
