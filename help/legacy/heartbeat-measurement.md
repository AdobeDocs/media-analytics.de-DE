---
title: Über Heartbeat-Messungen
description: Erfahren Sie, wie Heartbeats zur Erfassung von Videometriken verwendet werden.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e6c28e30-8689-4bf4-8fa8-561343d308a9
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# Über Heartbeat-Messungen

Adobe-Streaming-Mediendienste verwenden „Heartbeats“ zur Erfassung von Videometriken. Während der Videowiedergabe werden Heartbeats an den Heartbeat-Tracking-Server gesendet, um die Wiedergabedauer zu messen. Die Heartbeat-Aufrufe werden alle zehn Sekunden gesendet. Heartbeats führen zu granularen Videointeraktionsmetriken und präziseren Video-Fallout-Berichten. Streaming-Mediendienste messen Heartbeats unter Verwendung von Adobe Launch mit der Media Analytics-Erweiterung, der Media SDK und der Mediensammlungs-API. Die Komponenten `AppMeasurement` und `VisitorID` werden zum Empfangen von Videodaten verwendet.

Die Verwendung von Heartbeats in Streaming-Mediendiensten bietet die folgenden Vorteile:

| Funktion | Beschreibung |
|---|---|
| Medienereignisse | Detaillierte und benutzerdefinierte Ereignisse werden alle zehn Sekunden für Hauptinhalte und jede Sekunde für Anzeigen gesendet. |
| Metriken und Dimensionen | Klare, standardisierte Metriken, Dimensionen und Benchmarks für alle Anbieter. Mit einer standardisierten Lösung für alle Plattformen können Sie konsistente, standardisierte Variablen für alle Medien und Plattformen verwenden, um einen effizienteren Vergleich zwischen Kampagnen, Geräten und Anbietern zu ermöglichen. |
| Integrationen | Die Experience Cloud-ID ist mit Adobe Experience Cloud verknüpft, um eine Kreuzanalyse zu erleichtern. Mit der automatischen Adobe Experience Cloud-Integration können Sie Ihre Medien-Audiences segmentieren, diese ansprechen und Medienempfehlungen basierend auf den Benutzereinstellungen geben. |
| Preise | Transparentes Tracking jedes Medien-Streams (einzeln) |
| Implementierung und Support | Optimierte Konfiguration mit fortlaufenden Aktualisierungen und Verbesserungen. Mit einem optimierten Implementierungsprozess können Sie schnell Variablen über Ihre Player-API zuordnen und Implementierungen mit dem Adobe Debug-Tool validieren, um sicherzustellen, dass alle erforderlichen Variablen genau verfolgt werden. |
| Partnerfreigabe | Federated Media und Certified Metrics. Mit gemeinsam genutzten Daten über Federated Media können Sie unsere branchenführenden Medien-Sharing-Funktionen nutzen, um Daten über alle Ihre Medienverteilungspartner - Betreiber, Programmierer und Distributoren - hinweg ganzheitlich auszuwerten. |
| Erweitertes Tracking | Tracking heruntergeladener Inhalte, Tracking der Fehlerbehebung und gleichzeitige Betrachter. Sie können Streaming-Medieninhalte verfolgen, die auf ein Gerät heruntergeladen und auf diesem wiedergegeben werden, unabhängig von dessen Konnektivität. |
