---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung der Streaming-Mediensammlung mit Implementierungen, die nur auf Adobe Analytics oder Edge basieren
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 10%

---

# Voraussetzungen für Edge-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen gelten speziell für die Implementierung der Adobe-Streaming-Mediensammlung in Edge-Implementierungen.

1. **Vervollständigen Sie die allgemeinen Voraussetzungen**<br>
Unabhängig davon, ob Sie die Streaming-Mediensammlung für Implementierungen auf Adobe Analytics-Basis oder für Edge-Implementierungen implementieren, stellen Sie sicher, dass Sie die [allgemeinen Voraussetzungen](/help/getting-started/prereqs.md) erfüllen.

1. **Vergewissern Sie sich, dass Sie eine Adobe-Lösung implementieren, die mit Edge Network und der Streaming Media Collection kompatibel ist**<br>
Bei der Implementierung der Streaming Media Collection mit Edge müssen Sie auch über eine funktionierende Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer oder eine Real-time Customer Data Platform-Implementierung verfügen. Weitere Informationen finden Sie in der folgenden Dokumentation:
   * [Handbuch für Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=de)
   * [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de)
   * [Dokumentation zu Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=de)
   * [Dokumentation zu Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=de)

1. **Abrufen der URL des Medien-Tracking-Servers**<br>
Fragen Sie Ihren Customer Journey Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementieren Sie die Streaming-Mediensammlung mit dem -Edge Network**<br>
Führen Sie die Schritte unter [Implementieren der Streaming-Mediensammlung mithilfe des -Edge Networks ](/help/implementation/edge/implementation-edge.md) aus.
