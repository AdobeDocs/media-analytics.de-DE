---
title: Über Heartbeat-Messungen
description: Erfahren Sie, wie Heartbeats zur Erfassung von Videometriken verwendet werden.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 30%

---

# Über die Heartbeat-Messung

Adobe Analytics verwendet &quot;Heartbeats&quot;, um Videometriken zu erfassen. Während der Videowiedergabe werden Heartbeats an den Heartbeat-Tracking-Server gesendet, um die Wiedergabedauer zu messen. Die Heartbeat-Aufrufe werden alle zehn Sekunden gesendet. Heartbeats führen zu granularen Videointeraktionsmetriken und präziseren Video-Fallout-Berichten. Adobe Analytics für Streaming-Medien misst Heartbeats mithilfe von Adobe Launch mit der Media Analytics-Erweiterung, dem Media SDK und der Media Collection API. Die Komponenten `AppMeasurement` und `VisitorID` werden zum Empfangen von Videodaten verwendet.

Die Verwendung von Heartbeats in Adobe Analytics für Streaming-Medien bietet folgende Vorteile:

| Funktion | Beschreibung |
|---|---|
| Medienereignisse | Detaillierte und benutzerdefinierte Ereignisse werden alle zehn Sekunden für Hauptinhalte und jede Sekunde für Anzeigen gesendet. |
| Metriken und Dimensionen | Klare, standardisierte Metriken, Dimensionen und Benchmarks für alle Anbieter. Mit einer standardisierten Lösung für alle Plattformen können Sie konsistente, standardisierte Variablen für alle Medien und Plattformen verwenden, um einen effizienteren Vergleich zwischen Kampagnen, Geräten und Anbietern zu ermöglichen. |
| Integrationen | Die Experience Cloud-ID ist mit Adobe Experience Cloud verknüpft, um eine benutzerübergreifende Analyse zu erleichtern. Durch die automatische Adobe Experience Cloud-Integration können Sie Ihre Medienzielgruppen segmentieren, Zielgruppen auswählen und Medienempfehlungen basierend auf den Benutzereinstellungen bereitstellen. |
| Preise | Transparentes Tracking jedes Medien-Streams (einzeln) |
| Implementierung und Support | Optimierte Konfiguration mit laufenden Aktualisierungen und Verbesserungen. Mit einem optimierten Implementierungsprozess können Sie schnell Variablen über Ihre Player-API zuordnen und Implementierungen mit dem Adobe Debug Tool validieren, um sicherzustellen, dass alle erforderlichen Variablen genau verfolgt werden. |
| Partnerfreigabe | Federated Analytics und zertifizierte Metriken. Mit freigegebenen Daten über Federated Analytics können Sie unsere branchenführenden Medien-Sharing-Funktionen nutzen, um die Daten aller Medienverteilungspartner - Betreiber, Programmierer und Distributoren - ganzheitlich zu evaluieren. |
| Erweitertes Tracking | Tracking von heruntergeladenen Inhalten, Tracking von Fehlerwiederherstellungen und gleichzeitigen Viewern. Sie können Streaming-Medieninhalte verfolgen, die auf ein Gerät heruntergeladen und wiedergegeben werden, unabhängig von dessen Konnektivität. |
