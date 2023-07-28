---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung von Streaming-Medien mit reinen Adobe Analytics-Implementierungen
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 16%

---

# Voraussetzungen für Edge-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen gelten speziell für die Implementierung von Streaming-Medien mit Edge-Implementierungen.

1. **Allgemeine Voraussetzungen erfüllen**<br>
Stellen Sie sicher, dass Sie die [Allgemeine Voraussetzungen](/help/getting-started/prereqs.md).

1. **Überprüfen Sie, ob Sie eine Adobe-Lösung implementieren, die mit Edge und Streaming Media kompatibel ist.**<br>
Bei der Implementierung von Streaming-Medien mit Edge müssen Sie auch über einen funktionierenden Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer oder eine Real-time Customer Data Platform-Implementierung verfügen. Weitere Informationen finden Sie in den folgenden Dokumentationsressourcen:
   * [Handbuch für Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=de)
   * [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de)
   * [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=de)
   * [Real-time Customer Data Platform-Dokumentation](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=de)

1. **Abrufen der Medien-Tracking-Server-URL**<br>
Fragen Sie Ihren Customer Journey Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Installieren von Media Analytics mit Edge**<br>
Führen Sie die Schritte unter [Installieren von Media Analytics mit Experience Platform Edge](/help/implementation/edge/implementation-edge.md).