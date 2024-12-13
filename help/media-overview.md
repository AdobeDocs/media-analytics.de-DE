---
title: Übersicht über die Adobe-Streaming-Mediensammlung
description: Verwenden Sie die Sammlung von Streaming-Medien, um wichtige Einblicke in Inhalte, Audio und Werbung zu erhalten.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 65%

---

# Übersicht über die Adobe-Streaming-Mediensammlung

![Banner](./assets/media_analytics_banner.png)

Die Adobe-Streaming-Mediensammlung bietet leistungsstarke Erfassungs-, Mess- und Personalisierungs-Tools für Streaming-Medieninhalte wie Audio, Video und Werbung für Streaming-Medienanbieter. Sie können Metriken von Streaming-Medien mit Funktionen wie Audience Analytics, Mobile oder geräteübergreifenden Analysen kombinieren.

Streaming-Mediendaten lassen sich problemlos in die folgenden Adobe Experience Platform-Produkte integrieren:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Wenden Sie sich zur Implementierung der Streaming Media Collection an Ihren Adobe-Kundenbetreuer oder Ihr Adobe-Accountteam, um sicherzustellen, dass das Add-on für die Streaming Media Collection Teil Ihres Produktportfolios ist.

## Wichtigste Funktionen

Zu den Vorteilen der Streaming-Mediensammlung gehören Echtzeit-Monitoring, detaillierte Analyse, umsetzbare Einblicke, Monetarisierungsmöglichkeiten und mehr.

* **Echtzeit-Analyse**: Treffen Sie fundierte Entscheidungen in Echtzeit, indem Sie wichtige Leistungsmetriken wie Medienstarts kanalübergreifend verwenden.

  Mit der Streaming-Mediensammlung erhalten Sie nahezu in Echtzeit granulare Details zur Dauer, zu Stopps und Starts, mit denen Sie Video- und Audiometriken auswerten und kombinieren können. Diese Erkenntnisse ermöglichen es Ihnen, die Seh- und Hörgewohnheiten Ihrer Kundinnen und Kunden zu verstehen und mit hochgradig personalisierten Empfehlungen die Interaktion zu steigern.

* **Förderung der Interaktion**: Die Interaktion der Benutzenden wird gefördert, indem die Pufferung verringert wird und ermittelt wird, wo und wann Anzeigen in Inhalten abgespielt werden sollten, um ein reibungsloses, weniger störendes Erlebnis zu bieten, das zu Wiederholungsbesuchen führt.

* **Ganzheitliche Übersicht:** Kombinieren Sie verschiedene Datenpunkte Ihrer Inhaltsdistributorinnen und -distributoren, um eine umfassende Übersicht all Ihre Medienaktivitäten zu erhalten und die Interaktion und Aufrufe über alle Kanäle hinweg zu messen.

  Die Streaming Media Collection ermöglicht es Ihnen, das vollständige Kunden-Journey auf Ihrer Site und in Streaming-Apps zu verfolgen, um den Kundenpfad und die Kundeninteressen zu visualisieren und erweiterte Empfehlungen bereitzustellen sowie Kundenerlebnisse zu personalisieren.  Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente kategorisieren und alle Metadaten erfassen, die Sie für eine vollständige und detaillierte Analyse benötigen. Anschließend können Sie Daten analysieren und Erfolgskriterien den vollständig genutzten Medien, der durchschnittlich verbrachten Zeit und an abgeschlossenen Anzeigen zuordnen.

* **Wichtige Metriken**: Sie können wichtige Bereitstellungsmetriken in Bezug auf die Erlebnisqualität (Quality of Experience, QoE) messen, z. B. ausgelassene Frames, Pufferzeit und durchschnittliche Bit-Rate.

* **Erhöhte Granularität**: Bewerten Sie das Ansichtsverhalten auf einer extrem detaillierten Ebene, einschließlich der Besuchszeit einzelner Benutzer, gleichzeitige Betrachter/Zuhörer nach Minuten und der durchschnittlichen Konsumdauer des Inhalts.

* **Präzise Messung**: Führen Sie Messungen auf zahlreichen für den Medienkonsum verwendeten Geräten durch, einschließlich OTT, Smartphone, Tablet, Desktop, um Interaktionsmuster und -gewohnheiten der Benutzer zu überwachen.

* **Segmentierung**: Wenden Sie Klassifizierungen auf Ihre Player, Geräte, Genres und Kapitel an und zeigen Sie, wie sich diese auf Ihre gesamten Aufrufe und Kundeninteraktionen mit Inhalten, Audio, Anzeigen und kombinierten Inhalten auswirken.


## Funktionsweise

Die Tracking-Daten von Streaming-Medien werden von einem Player mithilfe von Media for Edge Network-SDK/Erweiterung, Media-Erweiterung mit Tags, Media-SDKs, Media Edge-API oder Media Collection-API erfasst.

Alle granularen Daten (bis zu 10 Sekunden) werden entweder an den Media Analytics-Dienst oder an Experience Edge gesendet (je nach gewählter [Implementierungsmethode](/help/implementation/overview.md)), die die Daten für jede einzelne Wiedergabesitzung erfassen und verarbeiten.

Nach dem Ende einer Wiedergabesitzung werden die berechneten Tracking-Daten zur Speicherung und zum Reporting entweder an Adobe Analytics oder an Customer Journey Analytics gesendet.

>[!NOTE]
>
>Bei Customer Journey Analytics-Implementierungen können Daten entweder über Experience Edge oder über Analytics Data Connector (ADC) an Customer Journey Analytics gesendet werden.


Ausführliche Informationen zu den verschiedenen Implementierungsmethoden finden Sie unter [Implementieren der Streaming Media Collection für Adobe Analytics oder Customer Journey Analytics](/help/implementation/overview.md).
