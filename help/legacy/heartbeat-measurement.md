---
title: Über Heartbeat-Messungen
description: Erfahren Sie, wie Heartbeats zur Erfassung von Videometriken verwendet werden.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 75%

---

# Über Heartbeat-Messungen

Adobe-Streaming-Mediendienste verwenden „Heartbeats“ zur Erfassung von Videometriken. Während der Videowiedergabe werden Heartbeats an den Heartbeat-Tracking-Server gesendet, um die Wiedergabedauer zu messen. Die Heartbeat-Aufrufe werden alle zehn Sekunden gesendet. Heartbeats führen zu granularen Videointeraktionsmetriken und präziseren Video-Fallout-Berichten. Streaming-Mediendienste messen Heartbeats unter Verwendung von Adobe Launch mit der Media Analytics-Erweiterung, der Media SDK und der Mediensammlungs-API. Die Komponenten `AppMeasurement` und `VisitorID` werden zum Empfangen von Videodaten verwendet.

Die Verwendung von Heartbeats in Streaming-Mediendiensten bietet die folgenden Vorteile:

| Funktion | Beschreibung |
|---|---|
| Medienereignisse | Detaillierte und benutzerdefinierte Ereignisse werden alle zehn Sekunden für Hauptinhalte und jede Sekunde für Anzeigen gesendet. |
| Metriken und Dimensionen | Klare, standardisierte Metriken, Dimensionen und Benchmarks für alle Anbieter. Mit einer standardisierten Lösung für alle Plattformen können Sie konsistente, standardisierte Variablen für alle Medien und Plattformen verwenden, was einen effizienteren Vergleich zwischen Kampagnen, Geräten und Anbietern ermöglicht. |
| Integrationen | Die Experience Cloud-ID ist mit Adobe Experience Cloud verknüpft, um eine übergreifende Analyse zu erleichtern. Dank der automatischen Adobe Experience Cloud-Integration können Sie Ihre Medien-Zielgruppen segmentieren, diese ansprechen und Medienempfehlungen basierend auf den Vorlieben der Benutzenden bereitstellen. |
| Preise | Transparentes Tracking jedes Medien-Streams (einzeln) |
| Implementierung und Support | Optimierte Konfiguration mit fortlaufenden Aktualisierungen und Verbesserungen. Mit einem optimierten Implementierungsprozess können Sie schnell Variablen über Ihre Player-API zuordnen und Implementierungen mit dem Adobe Debugging-Tool validieren, um sicherzustellen, dass alle erforderlichen Variablen präzise verfolgt werden. |
| Partnerfreigabe | Federated Media und Certified Metrics. Mit gemeinsam genutzten Daten über Federated Media können Sie unsere branchenführenden Medien-Sharing-Funktionen nutzen, um Daten über alle Ihre Medienverteilungspartner - Betreiber, Programmierer und Distributoren - hinweg ganzheitlich auszuwerten. |
| Erweitertes Tracking | Tracking von heruntergeladenen Inhalten, Tracking von Fehlerbehebungen und gleichzeitigen Betrachtern. Sie können Inhalte von Streaming-Medien nachverfolgen, die auf ein Gerät heruntergeladen und auf diesem wiedergegeben werden – unabhängig von dessen Konnektivität. |
