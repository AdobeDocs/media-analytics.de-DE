---
title: Voraussetzungen für reine Adobe Analytics-Implementierungen
description: Erfahren Sie mehr über die Voraussetzungen für die Verwendung des Streaming Media Collection Add-ons mit reinen Adobe Analytics-Implementierungen oder Edge-Implementierungen
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 10%

---

# Voraussetzungen für Edge-Implementierungen

Die in diesem Abschnitt beschriebenen Voraussetzungen gelten speziell für die Implementierung des Adobe Streaming Media Collection Add-ons mit Edge-Implementierungen.

1. **Allgemeine Voraussetzungen erfüllen**<br>
Stellen Sie sicher, dass Sie die Variable [Allgemeine Voraussetzungen](/help/getting-started/prereqs.md).

1. **Bestätigen Sie, dass Sie eine mit Edge Network und dem Add-on für die Streaming-Mediensammlung kompatible Adobe-Lösung implementieren.**<br>
Bei der Implementierung des Streaming-Mediensammlungs-Add-ons mit Edge müssen Sie auch über eine funktionierende Customer Journey Analytics-, Adobe Analytics-, Adobe Journey Optimizer- oder Real-time Customer Data Platform-Implementierung verfügen. Weitere Informationen finden Sie in den folgenden Dokumentationsressourcen:
   * [Handbuch für Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=de)
   * [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de)
   * [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=de)
   * [Real-time Customer Data Platform-Dokumentation](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=de)

1. **Abrufen der Medien-Tracking-Server-URL**<br>
Fragen Sie Ihren Customer Journey Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementieren des Add-ons für Streaming-Mediensammlung mit dem Edge Network**<br>
Führen Sie die Schritte unter [Implementieren des Add-ons für Streaming-Mediensammlung mit dem Edge Network](/help/implementation/edge/implementation-edge.md).
