---
title: Welche Wege stehen zur Implementierung von Streaming-Medien zur Verfügung?
description: Erfahren Sie mehr über Adobe Streaming Media-Implementierungspfade, einschließlich Datenerfassung in Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/U9PBQc7dHNmONZc06t1Xi7EITkveGUkzcst6Sakqqzo
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 676
ht-degree: 87%

---

# Implementierungspfade {#implementation-paths}

**DIESER INHALT WURDE IN DIE AKTUELLE IMPLEMENTIERUNGSPFADDATEI VERSCHOBEN**

Für jeden Implementierungspfad müssen sich Kunden an ihren Kundenbetreuer oder ihr Adobe-Account-Team wenden, um einen neuen Kundenauftrag zu unterzeichnen, da die Customer Journey Analytics Streaming Media Collection und Adobe Analytics für Streaming Media über eine eindeutige SKU verfügen und sich von einem auf Server-Aufrufen basierenden Preismodell zu einem auf Video-Streams basierenden Modell ändern.

## Datenerfassung in Adobe Experience Platform mit der Adobe Media Analytics-Erweiterung

>[!NOTE]
>Adobe Experience Platform Launch wurde umbenannt und umfasst eine Suite von Datenerfassungstechnologien in Experience Platform. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen vorgenommen. Eine Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).


Tags in Adobe Experience Platform sind die nächste Generation von Funktionen für das Tag-Management von Adobe. Tags bieten Kunden eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse notwendig sind. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten.

Tags ermöglichen jedem das Aufbauen und Verwalten eigener Integrationen (auch Erweiterungen genannt). Diese Erweiterungen stehen Adobe Experience Cloud-Kunden in einer App-Store-Oberfläche zur Verfügung, damit sie ihre Tags schnell installieren, konfigurieren und bereitstellen können.

Eine Erweiterung ist ein Paket mit Code (JavaScript, HTML und CSS) zur Erweiterung der Tag-Funktionalität. Erstellen, verwalten und aktualisieren Sie Ihre Integrationen mithilfe einer praktischen Self-Service-Oberfläche. Sie können sich Erweiterungen als Programme vorstellen, mit denen Sie Ihre Aufgaben erledigen.Weitere Informationen finden Sie im Artikel *Übersicht über Tags* in der [Adobe Experience Platform-Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=de)

Mit der Adobe Media Analytics-Erweiterung (MA) wird das JavaScript Media SDK (Media 2.x SDK) für Audio und Video hinzugefügt. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der `MediaHeartbeat`-Tracker-Instanz zu einer Site oder einem Projekt mit Datenerfassung.

Adobe-Datenerfassung mit der Media Analytics-Erweiterung erfordert Folgendes:
* Sie müssen Adobe Experience Cloud-Kunde sein.
* Sie müssen den Datenerfassungs- oder DTM-Einbettungs-Code auf Ihren Web-Seiten bereitstellen.
* [Analytics-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=de)
* [Experience Cloud ID-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=de)


## Client-Seite

Dies sind reine Media Analytics-Integrationen. Sie können das Video Heartbeat SDK und/oder die Media Collection API-Integrationen auswählen. Dieser Pfad kann für alle Video-Player verwendet werden, einschließlich Kunden- und/oder OVP-Player wie Brightcove, Ooyala und thePlatform.

Wenn Sie sich für Media Analytics entschieden haben, informieren Sie sich über die [Media SDK-Implementierung](/help/legacy/setup/legacy-setup-overview.md) und die [Media Collection API.](/help/implementation/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Um Media Analytics zu nutzen, müssen Kunden auch Adobe Analytics verwenden.

## Adobe Primetime

Adobe Primetime ist eine Adobe Experience Cloud-Lösung, mit der Inhaltsprogrammierer und -anbieter Medien auf allen vernetzten Bildschirmen monetarisieren können.

Primetime bietet eine modulare Plattform für die Videoveröffentlichung, Werbung, Personalisierung und Analyse und vereinfacht dadurch das geräteübergreifende Targeting, Monetarisieren und Aktivieren globaler Zielgruppen. Darüber hinaus bieten Primetime-Lösungen folgende Vorteile:

* Unterstützung einer präzisen Messung von Linear- und VOD-Content-Typen.
* Unterstützung der Messung von Werbeunterbrechungen mit (oder ohne) dynamischer Ad Insertion.
* Das nahtlose Ad-Insertion-Modell von TVSDK ermöglicht Analysen, die die Anzeigenwiedergabe direkt messen, wodurch die Genauigkeit steigt.
* Eine große Auswahl an Ereignissen und Metadaten gewährleistet die präzise Aufzeichnung von Problemen mit der QoS-Pufferung oder der mobilen Konnektivität sowie von Endbenutzerinteraktionen auf Mobilgeräten wie dem Suchen, Anhalten und Verschieben von Apps in den Hintergrund.
* Integrierte Unterstützung für Nielsen DTVR (linear) mit ID3-Metadaten und DCR mit CMS-Metadaten.


TVSDK ist bereits in das Media Analytics-SDK (Heartbeats) integriert, was die Implementierung auf allen unterstützen Plattformen deutlich vereinfacht und beschleunigt. Befolgen Sie zur Nutzung von Primetime die gleichen Richtlinien und Voraussetzungen wie auf der [Client-Seite](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md) sowie die folgenden Dokumente für Ihre Plattform(en): [Benutzerhandbuch zu Primetime](https://helpx.adobe.com/de/support/primetime.html).

Von Ihrem Kundenbetreuer/Account-Manager erhalten Sie Informationen zum Kauf von TVSDK.
