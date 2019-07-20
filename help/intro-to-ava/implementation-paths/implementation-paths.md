---
seo-title: Implementierungspfade
title: Implementierungspfade
uuid: 8400 c 938-e 77 e -4 c 88-b 23 b -5 f 5977 a 5316 c
translation-type: tm+mt
source-git-commit: ca7e63d9af1f84c7d5d620c72df5f62555f68c03

---


# Implementierungspfade {#implementation-paths}

Media Analytics (Heartbeats) ist die standardisierte Videolösung von Adobe. Sie hat das ältere Meilensteinmodell ersetzt.

Für jedes dieser Implementierungspfade müssen Kunden ihren Vertriebsvertreter/Kundenbetreuer kontaktieren, um eine neue Verkaufsbestellung zu signieren, da Media Analytics über eine eindeutige SKU und Änderungen von einem Preismodell basiert, das auf Serveraufrufen basierend auf Videostreams basiert:

* **Clientseitig -** Es handelt sich hierbei um Integrationen von Media Analytics. Sie können zwischen dem Video Heartbeat SDK und/oder den Mediensammlungs-API-Integrationen wählen. Dieser Pfad kann über alle Videoplayer hinweg verwendet werden, einschließlich Kunden- und/oder OVP-Player, z. B. Brightcove, Ooyala, thePlatform usw.

   If Media Analytics is your intended path, see the [Media SDK Implementation](../../sdk-implement/setup/setup-overview.md) and the [Media Collection API.](../../media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Um Media Analytics verwenden zu können, müssen Kunden auch Adobe Analytics verwenden.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch, das nachfolgende Produkt zum Dynamischen Tag-Management, bietet eine Media Analytics Launch Extension, die die Implementierung der Videoverfolgung in Ihren Playern erleichtert.

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime:** Adobe Primetime ist eine Adobe Experience Cloud-Lösung, die Content-Programmierer und -verteiler bei der Monetarisierung von Medien auf jedem verbundenen Bildschirm unterstützt.

   Mithilfe einer modularen Plattform für Video-Publishing, Werbung, Personalisierung und Analysen beseitigt Primetime die Komplexität beim Erreichen, Ansprechen und Monetarisieren globaler Zielgruppen auf verschiedenen Geräten. Darüber hinaus bietet Primetime folgende Lösungen und Vorteile:

   * Unterstützung für präzise Messungen von linearen und VOD-Content-Typen.
   * Unterstützung für die Messung von Werbeunterbrechungen mit (oder ohne) Dynamic Ad Insertion.
   * Das nahtlose Ad-Insertion-Modell von TVSDK ermöglicht Analysen, die die Anzeigenwiedergabe direkt messen und so die Genauigkeit steigern können.
   * Umfangreiche Ereignisse und Metadaten, um die Genauigkeit bei der Messung von QoS, Puffern und Unterbrechungen mobiler Datenverbindungen sowie von Anwenderinteraktionen, z. B. Suche, Pause und das Ausführen der App im Hintergrund, zu gewährleisten.
   * Integrierte Unterstützung für Nielsen DTVR (linear) mit ID3- und DCR mit CMS-Metadaten.
   TVSDK ist bereits in das Media Analtyics (Heartbeats) SDK integriert, wodurch die Implementierung für jede unterstützte Plattform viel einfacher und schneller wird. Primetime unterstützt darüber hinaus die Partnerschaft mit Nielsen. Um Primetime zu verwenden, beachten Sie die Anweisungen und Voraussetzungen in  [ Client-seitig](../../intro-to-ava/implementation-paths/client-side-path.md) sowie die folgenden Dokumente für Ihre Plattform(en): [Primetime-Benutzerhandbuch.](https://helpx.adobe.com/primetime/user-guide.html)

   Von Ihrem Support-Mitarbeiter/Account-Manager erhalten Sie Informationen zum Kauf von TVSDK.
