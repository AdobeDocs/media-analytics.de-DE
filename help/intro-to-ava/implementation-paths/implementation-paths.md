---
title: Welche Pfade zur Implementierung von Streaming-Medien stehen zur Verfügung?
description: Erfahren Sie mehr über Adobe Streaming Media-Implementierungspfade einschließlich Adobe Launch.
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 87%

---


# Implementierungspfade {#implementation-paths}

Für jeden Implementierungspfad müssen Kunden sich an ihren Vertriebsmitarbeiter/Kundenbetreuer wenden, um eine neue Bestellung zu unterzeichnen, da Streaming Media Analytics eine eindeutige SKU aufweist und Änderungen von einem Preismodell auf der Grundlage von Serveraufrufen zu einem auf Video-Streams basierenden Modell vorgenommen werden.

* **Adobe Launch mit der Adobe Media Analytics-Erweiterung**

   Adobe Launch ist die Adobe-Tag-Management-Lösung der nächsten Generation von Adobe. Launch bietet eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse erforderlich sind. Um Ihre eigenen Integrationen mit Launch zu erstellen und zu pflegen, verwenden Sie Erweiterungen. Eine Erweiterung ist ein JavaScript-, HTML- und CSS-Package, das die Launch-Benutzeroberfläche und die Client-Funktionen ausbaut. Weitere Informationen finden Sie im [Benutzerhandbuch zu Experience Platform Launch](https://docs.adobe.com/content/help/de-DE/launch/using/overview.html)

   Mit der Adobe Media Analytics-Erweiterung (MA) wird das JavaScript Media SDK (Media 2.x SDK) für Audio und Video hinzugefügt. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der `MediaHeartbeat`-Tracker-Instanz zu einer Launch-Site oder einem Projekt.

   Adobe Launch mit der Media Analytics-Erweiterung erfordert Folgendes:
   * Sie müssen Adobe Experience Cloud-Kunde sein.
   * Sie müssen den Launch- oder DTM-Einbettungscode auf Ihren Websites bereitstellen.
   * [Analytics-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Client-seitig -** Dies sind reine Media Analytics-Integrationen. Sie können das Video Heartbeat SDK und/oder die Media Collection API-Integrationen auswählen. Dieser Pfad kann für alle Video-Player verwendet werden, einschließlich Kunden- und/oder OVP-Player wie Brightcove, Ooyala und thePlatform.

   Wenn Sie sich für Media Analytics entschieden haben, informieren Sie sich über die [Media SDK-Implementierung](/help/sdk-implement/setup/setup-overview.md) und die [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Um Media Analytics zu nutzen, müssen Kunden auch Adobe Analytics verwenden.

* **Adobe Primetime:** Adobe Primetime ist eine Adobe Experience Cloud-Lösung, mit der Inhaltsprogrammierer und -distributoren Medien auf allen vernetzten Geräten monetarisieren können.

   Primetime bietet eine modulare Plattform für die Videoveröffentlichung, Werbung, Personalisierung und Analyse und vereinfacht dadurch das geräteübergreifende Targeting, Monetarisieren und Aktivieren globaler Audiences. Darüber hinaus bieten Primetime-Lösungen folgende Vorteile:

   * Unterstützung einer präzisen Messung von Linear- und VOD-Content-Typen.
   * Unterstützung der Messung von Werbeunterbrechungen mit (oder ohne) dynamischer Ad Insertion.
   * Das nahtlose Ad-Insertion-Modell von TVSDK ermöglicht Analysen, die die Anzeigenwiedergabe direkt messen, wodurch die Genauigkeit steigt.
   * Eine große Auswahl an Ereignissen und Metadaten gewährleistet die präzise Aufzeichnung von Problemen mit der QoS-Pufferung oder der mobilen Konnektivität sowie von Endbenutzerinteraktionen auf Mobilgeräten wie dem Suchen, Anhalten und Verschieben von Apps in den Hintergrund.

<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK ist bereits in das Media Analytics-SDK (Heartbeats) integriert, was die Implementierung auf allen unterstützen Plattformen deutlich vereinfacht und beschleunigt. <!--Primetime also supports the partnership with Nielsen.--> Befolgen Sie zur Nutzung von Primetime die gleichen Richtlinien und Voraussetzungen wie auf der [Clientseite](/help/intro-to-ava/implementation-paths/client-side-path.md) sowie die folgenden Dokumente für Ihre Plattform(en): [Primetime-Benutzerhandbuch.](https://helpx.adobe.com/de/support/primetime.html)

Von Ihrem Support-Mitarbeiter/Account-Manager erhalten Sie Informationen zum Kauf von TVSDK.
