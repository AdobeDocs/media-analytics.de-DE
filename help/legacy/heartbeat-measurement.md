---
title: Über Heartbeat-Messungen
description: Erfahren Sie, wie Heartbeats zur Erfassung von Videometriken verwendet werden.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: 0079116bcf39bb6d20b4fd5f14bd3c19137c46e3
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 75%

---

# Über Heartbeat-Messungen

Die hinzufügen-On der Adobe Systems Streaming Media Collection verwendet &quot;Heartbeats&quot; zum Erfassen von Videometriken. Während der Videowiedergabe werden Heartbeats an den Heartbeat-Tracking-Server gesendet, um die Wiedergabedauer zu messen. Die Heartbeat-Aufrufe werden alle zehn Sekunden gesendet. Heartbeats führen zu granularen Videointeraktionsmetriken und präziseren Video-Fallout-Berichten. Streaming Media misst Heartbeats mithilfe von Adobe Systems Launch mit der Media Analytics Erweiterung, dem Media SDK und der Media Collection API. Die Komponenten `AppMeasurement` und `VisitorID` werden zum Empfangen von Videodaten verwendet.

Die Verwendung von Heartbeats in der Streaming Media-Sammlung hinzufügen-on bietet die folgenden Vorteile:

| Funktion | Beschreibung |
|---|---|
| Medienereignisse | Detaillierte und benutzerdefinierte Ereignisse werden alle zehn Sekunden für Hauptinhalte und jede Sekunde für Anzeigen gesendet. |
| Metriken und Dimensionen | Klare, standardisierte Metriken, Dimensionen und Benchmarks für alle Anbieter. Mit einer standardisierten Lösung für alle Plattformen können Sie konsistente, standardisierte Variablen für alle Medien und Plattformen verwenden, was einen effizienteren Vergleich zwischen Kampagnen, Geräten und Anbietern ermöglicht. |
| Integrationen | Die Experience Cloud-ID ist mit Adobe Experience Cloud verknüpft, um eine übergreifende Analyse zu erleichtern. Dank der automatischen Adobe Experience Cloud-Integration können Sie Ihre Medien-Zielgruppen segmentieren, diese ansprechen und Medienempfehlungen basierend auf den Vorlieben der Benutzenden bereitstellen. |
| Preise | Transparentes Tracking jedes Medien-Streams (einzeln) |
| Implementierung und Support | Optimierte Konfiguration mit fortlaufenden Aktualisierungen und Verbesserungen. Mit einem optimierten Implementierungsprozess können Sie schnell Variablen über Ihre Player-API zuordnen und Implementierungen mit dem Adobe Debugging-Tool validieren, um sicherzustellen, dass alle erforderlichen Variablen präzise verfolgt werden. |
| Partnerfreigabe | Federated Media und zertifizierte Metriken. Mit freigegebenen Daten über Federated Media können Sie von unseren branchenweit ersten Medien-Sharing-Funktionen profitieren, um Daten ganzheitlich über alle Ihre Medien Vertriebspartner hinweg zu bewerten – Betreiber, Programmierer und Distributoren. |
| Erweitertes Tracking | Tracking von heruntergeladenen Inhalten, Tracking von Fehlerbehebungen und gleichzeitigen Betrachtern. Sie können Inhalte von Streaming-Medien nachverfolgen, die auf ein Gerät heruntergeladen und auf diesem wiedergegeben werden – unabhängig von dessen Konnektivität. |
