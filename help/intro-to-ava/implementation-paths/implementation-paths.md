---
seo-title: Implementierungspfade
title: Implementierungspfade
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementierungspfade {#implementation-paths}

Media Analytics (Heartbeats) ist die standardisierte Videolösung von Adobe. Sie hat das ältere Meilensteinmodell ersetzt.

Für jeden dieser Implementierungspfade müssen Kunden sich an ihren Vertriebsmitarbeiter/Kundenbetreuer wenden, um eine neue Bestellung zu unterzeichnen, da Media Analytics eine eindeutige SKU besitzt und Änderungen von einem Preismodell auf der Grundlage von Serveraufrufen zu einem auf Video-Streams basierenden Modell vorgenommen werden:

* **Client-Seite -** Dies sind ausschließlich Media Analytics-Integrationen. Sie können zwischen dem Video Heartbeat SDK und/oder den Mediensammlungs-API-Integrationen wählen. Dieser Pfad kann über alle Videoplayer hinweg verwendet werden, einschließlich Kunden- und/oder OVP-Player, z. B. Brightcove, Ooyala, thePlatform usw.

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Zur Verwendung von Media Analytics müssen Kunden auch Adobe Analytics verwenden.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch, das Folgeprodukt zum dynamischen Tag-Management, verfügt über eine Media Analytics Launch Extension, die die Implementierung der Videoverfolgung in Ihren Playern erleichtert.

   Weitere Informationen zum Start der Erlebnisplattform finden Sie hier: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime -** Adobe Primetime ist eine Adobe Experience Cloud-Lösung, mit der Programmierer und Distributoren von Inhalten bei der Monetarisierung von Medien auf jedem angeschlossenen Bildschirm unterstützt werden.

   Mithilfe einer modularen Plattform für Video-Publishing, Werbung, Personalisierung und Analysen beseitigt Primetime die Komplexität beim Erreichen, Ansprechen und Monetarisieren globaler Zielgruppen auf verschiedenen Geräten. Darüber hinaus bietet Primetime folgende Lösungen und Vorteile:

   * Unterstützung für präzise Messungen von linearen und VOD-Content-Typen.
   * Unterstützung für die Messung von Werbeunterbrechungen mit (oder ohne) Dynamic Ad Insertion.
   * Das nahtlose Ad-Insertion-Modell von TVSDK ermöglicht Analysen, die die Anzeigenwiedergabe direkt messen und so die Genauigkeit steigern können.
   * Umfangreiche Ereignisse und Metadaten, um die Genauigkeit bei der Messung von QoS, Puffern und Unterbrechungen mobiler Datenverbindungen sowie von Anwenderinteraktionen, z. B. Suche, Pause und das Ausführen der App im Hintergrund, zu gewährleisten.
   * Integrierte Unterstützung für Nielsen DTVR (linear) mit ID3- und DCR mit CMS-Metadaten.
   TVSDK ist bereits in das Media Analytics (Heartbeats) SDK integriert, was die Implementierung auf jeder unterstützten Plattform wesentlich einfacher und schneller macht. Primetime unterstützt darüber hinaus die Partnerschaft mit Nielsen. Um Primetime zu verwenden, beachten Sie die Anweisungen und Voraussetzungen in  [ Client-seitig](/help/intro-to-ava/implementation-paths/client-side-path.md) sowie die folgenden Dokumente für Ihre Plattform(en): [Primetime-Benutzerhandbuch.](https://helpx.adobe.com/primetime/user-guide.html)

   Von Ihrem Support-Mitarbeiter/Account-Manager erhalten Sie Informationen zum Kauf von TVSDK.
