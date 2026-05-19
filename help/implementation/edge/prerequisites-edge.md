---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung der Streaming-Mediensammlung mit Implementierungen, die nur auf Adobe Analytics oder Edge basieren
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 19%

---

# Voraussetzungen für Edge-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen gelten speziell für die Implementierung der Adobe Streaming Media Collection mit Edge-Implementierungen.

1. **Allgemeine Voraussetzungen erfüllen**<br>
Unabhängig davon, ob Sie die Streaming-Mediensammlung für Implementierungen auf Adobe Analytics-Basis oder für Edge-Implementierungen implementieren, stellen Sie sicher, dass Sie die [allgemeinen Voraussetzungen](/help/getting-started/prereqs.md) erfüllen.

1. **Vergewissern Sie sich, dass Sie eine Adobe-Lösung implementieren, die mit Edge Network und der Streaming Media Collection kompatibel ist**<br>
Bei der Implementierung der Streaming-Mediensammlung mit Edge müssen Sie auch über eine funktionierende Implementierung von Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer oder Real-Time Customer Data Platform verfügen. Weitere Informationen finden Sie in der folgenden Dokumentation:
   * [Handbuch zu Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=de)
   * [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de)
   * [Dokumentation zu Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=de)
   * [Dokumentation zu Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=de)

1. **Abrufen der URL des Medien-Tracking-Servers**<br>
Fragen Sie Ihren Customer Journey Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementieren der Streaming-Mediensammlung mit der Edge Network**<br>
Führen Sie die Schritte unter [Implementieren der Streaming-Mediensammlung mithilfe der Edge Network](/help/implementation/edge/implementation-edge.md) aus.
