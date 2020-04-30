---
title: Implementierungspfade
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementierungspfade {#implementation-paths}

Bei Media Analytics (Heartbeats) handelt es sich um die standardisierte Videolösung von Adobe. Sie hat das ältere Meilensteinmodell ersetzt.

Für jeden dieser Implementierungspfade müssen sich Kunden an ihren Kundenbetreuer/Account-Manager wenden, um einen neuen Kundenauftrag zu unterzeichnen, da Media Analytics über eine eigene SKU verfügt und sich der Preis hier nicht aus den Server-Aufrufen, sondern aus den Video-Streams ergibt:

* **Client-seitig -** Dies sind reine Media Analytics-Integrationen. Sie können das Video Heartbeat SDK und/oder die Media Collection API-Integrationen auswählen. Dieser Pfad kann für alle Video-Player verwendet werden, einschließlich Kunden- und/oder OVP-Player wie Brightcove, Ooyala und thePlatform.

   Wenn Sie sich für Media Analytics entschieden haben, informieren Sie sich über die [Media SDK-Implementierung](/help/sdk-implement/setup/setup-overview.md) und die [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Um Media Analytics zu nutzen, müssen Kunden auch Adobe Analytics verwenden.

* **Adobe Experience Platform Launch:** Adobe Experience Platform Launch, das Nachfolgeprodukt von Dynamic Tag Management, verfügt über eine Media Analytics-Launch-Erweiterung, die die Implementierung von Video-Tracking in Ihren Playern erleichtert.

   Weitere Informationen zu Experience Platform Launch finden Sie hier: [Adobe Media Analytics for Audio and Video­Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime:** Adobe Primetime ist eine Adobe Experience Cloud-Lösung, mit der Inhaltsprogrammierer und -distributoren Medien auf allen vernetzten Geräten monetarisieren können.

   Primetime bietet eine modulare Plattform für die Videoveröffentlichung, Werbung, Personalisierung und Analyse und vereinfacht dadurch das geräteübergreifende Targeting, Monetarisieren und Aktivieren globaler Audiences. Darüber hinaus bieten Primetime-Lösungen folgende Vorteile:

   * Unterstützung einer präzisen Messung von Linear- und VOD-Content-Typen.
   * Unterstützung der Messung von Werbeunterbrechungen mit (oder ohne) dynamischer Ad Insertion.
   * Das nahtlose Ad-Insertion-Modell von TVSDK ermöglicht Analysen, die die Anzeigenwiedergabe direkt messen, wodurch die Genauigkeit steigt.
   * Eine große Auswahl an Ereignissen und Metadaten gewährleistet die präzise Aufzeichnung von Problemen mit der QoS-Pufferung oder der mobilen Konnektivität sowie von Endbenutzerinteraktionen auf Mobilgeräten wie dem Suchen, Anhalten und Verschieben von Apps in den Hintergrund.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK ist bereits in das Media Analytics-SDK (Heartbeats) integriert, was die Implementierung auf allen unterstützen Plattformen deutlich vereinfacht und beschleunigt. <!--Primetime also supports the partnership with Nielsen.--> Befolgen Sie zur Nutzung von Primetime die gleichen Richtlinien und Voraussetzungen wie auf der [Clientseite](/help/intro-to-ava/implementation-paths/client-side-path.md) sowie die folgenden Dokumente für Ihre Plattform(en): [Primetime-Benutzerhandbuch.](https://helpx.adobe.com/de/primetime/user-guide.html)

Von Ihrem Support-Mitarbeiter/Account-Manager erhalten Sie Informationen zum Kauf von TVSDK.
