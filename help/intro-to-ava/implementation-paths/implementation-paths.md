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

* **Client-seitig -** Dies sind reine Media Analytics-Integrationen. Sie können zwischen dem Video Heartbeat SDK und/oder den Mediensammlungs-API-Integrationen wählen. Dieser Pfad kann über alle Videoplayer hinweg verwendet werden, einschließlich Kunden- und/oder OVP-Player, z. B. Brightcove, Ooyala, thePlatform usw.

   Wenn Sie sich für Media Analytics entschieden haben, informieren Sie sich über die [Media SDK-Implementierung](/help/sdk-implement/setup/setup-overview.md) und die [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Um Media Analytics zu nutzen, müssen Kunden auch Adobe Analytics verwenden.

* **Adobe Experience Platform Launch:** Adobe Experience Platform Launch, das Nachfolgeprodukt von Dynamic Tag Management, verfügt über eine Media Analytics-Launch-Erweiterung, die die Implementierung von Video-Tracking in Ihren Playern erleichtert.

   Weitere Informationen zu Experience Platform Launch finden Sie hier: [Adobe Media Analytics for Audio and Video­Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime:** Adobe Primetime ist eine Adobe Experience Cloud-Lösung, mit der Inhaltsprogrammierer und -distributoren Medien auf allen vernetzten Geräten monetarisieren können.

   Mithilfe einer modularen Plattform für Video-Publishing, Werbung, Personalisierung und Analysen beseitigt Primetime die Komplexität beim Erreichen, Ansprechen und Monetarisieren globaler Zielgruppen auf verschiedenen Geräten. Darüber hinaus bietet Primetime folgende Lösungen und Vorteile:

   * Unterstützung für präzise Messungen von linearen und VOD-Content-Typen.
   * Unterstützung für die Messung von Werbeunterbrechungen mit (oder ohne) Dynamic Ad Insertion.
   * Das nahtlose Ad-Insertion-Modell von TVSDK ermöglicht Analysen, die die Anzeigenwiedergabe direkt messen und so die Genauigkeit steigern können.
   * Umfangreiche Ereignisse und Metadaten, um die Genauigkeit bei der Messung von QoS, Puffern und Unterbrechungen mobiler Datenverbindungen sowie von Anwenderinteraktionen, z. B. Suche, Pause und das Ausführen der App im Hintergrund, zu gewährleisten.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK ist bereits in das Media Analytics-SDK (Heartbeats) integriert, was die Implementierung auf allen unterstützen Plattformen deutlich vereinfacht und beschleunigt. <!--Primetime also supports the partnership with Nielsen.--> Befolgen Sie zur Nutzung von Primetime die gleichen Richtlinien und Voraussetzungen wie auf der [Clientseite](/help/intro-to-ava/implementation-paths/client-side-path.md) sowie die folgenden Dokumente für Ihre Plattform(en): [Primetime-Benutzerhandbuch.](https://helpx.adobe.com/de/primetime/user-guide.html)

Von Ihrem Support-Mitarbeiter/Account-Manager erhalten Sie Informationen zum Kauf von TVSDK.
