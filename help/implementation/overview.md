---
title: Implementieren von Streaming-Medien für Adobe Analytics oder Customer Journey Analytics
description: Erfahren Sie mehr über die Implementierungspfade von Streaming-Medien.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: ade20d7ae3cbb525b3a8390a27e1d93201d83003
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 13%

---

# Implementieren von Streaming-Medien für Adobe Analytics oder Customer Journey Analytics

Es gibt verschiedene Möglichkeiten, Streaming-Medien zu implementieren. Einen detaillierten Vergleich der unterstützten Geräte und Plattformen mit den auf dieser Seite beschriebenen Implementierungsmethoden finden Sie unter [Unterstützte Geräte und Plattformen](/help/getting-started/supported-devices.md).

## Edge-Implementierungsmethoden

In den meisten Fällen empfehlen wir die Verwendung von Edge bei der Implementierung von Media Analytics für alle neuen Adobe Analytics- oder Customer Journey Analytics-Kunden (CJA).

* **Media for Edge Network SDK/Erweiterung:** Erfasst Daten von iOS- und Android-Geräten und sendet sie an Edge. Daten können dann entweder an CJA oder Adobe Analytics gesendet werden.

  Weitere Informationen zum Media for Edge Network SDK/zur Erweiterung finden Sie unter [Installieren von Media Analytics mit Experience Platform Edge](/help/implementation/implementation-edge.md).

  >[!NOTE]
  >
  >Diese Implementierungsmethode unterstützt das Web SDK oder Roku derzeit nicht. Beide werden jedoch bei der Implementierung mit der Media Edge-API unterstützt.

* **Media Edge-API:** Kann angepasst werden, um Daten von beliebigen Geräten oder Formaten (einschließlich Mobilgeräten, Web- und Over-the-Top-Geräten) zu erfassen und Daten an Edge zu senden. Daten können dann entweder an CJA oder Adobe Analytics gesendet werden.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA-Workflow](assets/cja-implementation.png)

## Andere Implementierungsmethoden

In den meisten Fällen werden die oben beschriebenen Edge-Implementierungsmethoden sowohl für CJA als auch für Adobe Analytics empfohlen, insbesondere für neue Implementierungen.

Zusätzlich zu den Edge-Implementierungsmethoden sind weitere Implementierungsmethoden verfügbar. Diese Implementierungsmethoden wurden ursprünglich für die Verwendung mit Adobe Analytics entwickelt. Kunden mit einer der folgenden Implementierungsmethoden können jedoch weiterhin Daten in Customer Journey Analytics zur Verfügung stellen, indem sie eine [Analytics-Quellverbindung](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=de).

* **Media-Erweiterung mit Tags:** Die Adobe Medien Analytics für Audio und Video-Erweiterung bietet die Funktionalität zum Hinzufügen der Media-Tracker-Instanz zu einer Site oder einem Projekt, für die Tags aktiviert sind. Daten werden an Adobe Analytics gesendet.

  Informationen zum Installieren, Konfigurieren und Implementieren der Media-Erweiterung mit Tags finden Sie unter [Übersicht über die Erweiterung &quot;Adobe Medien Analytics (3.x SDK) for Audio and Video&quot;](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Medien-SDK:**  Daten werden an Adobe Analytics gesendet.

  Informationen zum Herunterladen und Installieren von Medien-SDKs und Erweiterungen finden Sie unter [Abrufen von Medien-SDKs, Erweiterungen mithilfe von Tags und OTT-SDKs](/help/getting-started/download-sdks.md).

* **Mediensammlungs-API:** Tracking von Audio- und Videoereignissen mit RESTful-HTTP-Aufrufen. Daten werden an Adobe Analytics gesendet.

  Informationen zur Verwendung der Mediensammlungs-APIs finden Sie unter [Mediensammlungs-APIs](media-collection-api/mc-api-overview.md).


![Analytics-Workflow](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
