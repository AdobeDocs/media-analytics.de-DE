---
title: Welche Wege stehen zur Implementierung von Streaming-Medien zur Verfügung?
description: Erfahren Sie mehr über Adobe Streaming Media-Implementierungspfade, einschließlich Datenerfassung in Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f88e8b02bc9723793822fa7647a2ceab9ada45e6
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 100%

---

# Implementierungspfade {#implementation-paths}

Für jeden Implementierungspfad müssen sich Kunden an ihren Kundenbetreuer/Konto-Manager wenden, um einen neuen Kundenauftrag zu unterzeichnen, da Streaming Media Analytics über eine eindeutige SKU verfügt und sich der Preis hier nicht aus den Server-Aufrufen, sondern aus den Video-Streams ergibt.

## Datenerfassung in Adobe Experience Platform mit der Adobe Media Analytics-Erweiterung

>[!NOTE]
>Adobe Experience Platform Launch wurde umbenannt und umfasst eine Suite von Datenerfassungstechnologien in Experience Platform. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen vorgenommen. Eine Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).


Tags in Adobe Experience Platform sind die nächste Generation von Funktionen für das Tag-Management von Adobe. Tags bieten Kunden eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse notwendig sind. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten.

Tags ermöglichen jedem das Aufbauen und Verwalten eigener Integrationen (auch Erweiterungen genannt). Diese Erweiterungen stehen Adobe Experience Cloud-Kunden in einer App-Store-Oberfläche zur Verfügung, damit sie ihre Tags schnell installieren, konfigurieren und bereitstellen können.

Eine Erweiterung ist ein Paket mit Code (JavaScript, HTML und CSS) zur Erweiterung der Tag-Funktionalität. Erstellen, verwalten und aktualisieren Sie Ihre Integrationen mithilfe einer praktischen Self-Service-Oberfläche. Sie können sich Erweiterungen wie Programme vorstellen, mit denen Sie Ihre Aufgaben erledigen. Weitere Informationen finden Sie unter *Übersicht über Tags* in der [Dokumentation zu Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=de)

Mit der Adobe Media Analytics-Erweiterung (MA) wird das JavaScript Media SDK (Media 2.x SDK) für Audio und Video hinzugefügt. Diese Erweiterung bietet die Funktionalität zum Hinzufügen der `MediaHeartbeat`-Tracker-Instanz zu einer Site oder einem Projekt mit Datenerfassung.

Adobe-Datenerfassung mit der Media Analytics-Erweiterung erfordert Folgendes:
* Sie müssen Adobe Experience Cloud-Kunde sein.
* Sie müssen den Datenerfassungs- oder DTM-Einbettungs-Code auf Ihren Web-Seiten bereitstellen.
* [Analytics-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=de)
* [Experience Cloud ID-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=de)


## Client-Seite

Dies sind reine Media Analytics-Integrationen. Sie können das Video Heartbeat SDK und/oder die Media Collection API-Integrationen auswählen. Dieser Pfad kann für alle Video-Player verwendet werden, einschließlich Kunden- und/oder OVP-Player wie Brightcove, Ooyala und thePlatform.

Wenn Sie sich für Media Analytics entschieden haben, informieren Sie sich über die [Media SDK-Implementierung](/help/sdk-implement/setup/setup-overview.md) und die [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Um Media Analytics zu nutzen, müssen Kunden auch Adobe Analytics verwenden.

## Adobe Primetime

Adobe Primetime ist eine Adobe Experience Cloud-Lösung, mit der Inhaltsprogrammierer und -distributoren Medien auf allen vernetzten Bildschirmen monetarisieren können.

Primetime bietet eine modulare Plattform für die Videoveröffentlichung, Werbung, Personalisierung und Analyse und vereinfacht dadurch das geräteübergreifende Targeting, Monetarisieren und Aktivieren globaler Audiences. Darüber hinaus bieten Primetime-Lösungen folgende Vorteile:

* Unterstützung einer präzisen Messung von Linear- und VOD-Content-Typen.
* Unterstützung der Messung von Werbeunterbrechungen mit (oder ohne) dynamischer Ad Insertion.
* Das nahtlose Ad-Insertion-Modell von TVSDK ermöglicht Analysen, die die Anzeigenwiedergabe direkt messen, wodurch die Genauigkeit steigt.
* Eine große Auswahl an Ereignissen und Metadaten gewährleistet die präzise Aufzeichnung von Problemen mit der QoS-Pufferung oder der mobilen Konnektivität sowie von Endbenutzerinteraktionen auf Mobilgeräten wie dem Suchen, Anhalten und Verschieben von Apps in den Hintergrund.
* Integrierte Unterstützung für Nielsen DTVR (linear) mit ID3- und DCR mit CMS-Metadaten.


TVSDK ist bereits in das Media Analytics-SDK (Heartbeats) integriert, was die Implementierung auf allen unterstützen Plattformen deutlich vereinfacht und beschleunigt. Befolgen Sie zur Nutzung von Primetime die gleichen Richtlinien und Voraussetzungen wie auf der [Client-Seite](/help/intro-to-ava/implementation-paths/client-side-path.md) sowie die folgenden Dokumente für Ihre Plattform(en): [Benutzerhandbuch zu Primetime](https://helpx.adobe.com/de/support/primetime.html).

Von Ihrem Kundenbetreuer/Account-Manager erhalten Sie Informationen zum Kauf von TVSDK.
