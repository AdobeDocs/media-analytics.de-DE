---
title: Übersicht über Adobe-Streaming-Medien
description: Verwenden Sie Adobe-Lösungen für Streaming-Medien, um leistungsstarke insight für Inhalte, Audio und Werbung zu erhalten.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 59%

---

# Übersicht über Adobe Streaming Media Services

![Banner](./assets/media_analytics_banner.png)

Adobe-Streaming-Mediendienste bieten leistungsstarke Erfassungs-, Mess- und Personalisierungs-Tools für Streaming-Medieninhalte wie Audio, Video und Werbung für Streaming-Medienanbieter. Sie können Metriken von Streaming-Medien mit Funktionen wie Audience Analytics, Mobile oder geräteübergreifenden Analysen kombinieren.

Streaming-Mediendaten lassen sich problemlos in die folgenden Adobe Experience Platform-Produkte integrieren:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Wenden Sie sich zur Implementierung der Streaming-Mediendienste an Ihren Adobe-Kundenbetreuer oder Ihr Adobe-Accountteam, um sicherzustellen, dass das Add-on &quot;Customer Journey Analytics Streaming Media Collection“ oder das Add-on „Adobe Analytics for Streaming Media“ Teil Ihres Produktportfolios ist.

## Wichtigste Funktionen

Zu den Vorteilen der Streaming-Medien-Services gehören Echtzeit-Monitoring, detaillierte Analyse, umsetzbare Einblicke, Monetarisierungsmöglichkeiten und mehr.

* **Echtzeit-Analyse**: Treffen Sie fundierte Entscheidungen in Echtzeit, indem Sie wichtige Leistungsmetriken wie Medienstarts kanalübergreifend verwenden.

  Mit den Streaming-Mediendiensten erhalten Sie nahezu in Echtzeit granulare Details zur Dauer, zu Stopps und Starts, mit denen Sie Video- und Audiometriken auswerten und kombinieren können. Diese Erkenntnisse ermöglichen es Ihnen, die Seh- und Hörgewohnheiten Ihrer Kundinnen und Kunden zu verstehen und mit hochgradig personalisierten Empfehlungen die Interaktion zu steigern.

* **Förderung der Interaktion**: Die Interaktion der Benutzenden wird gefördert, indem die Pufferung verringert wird und ermittelt wird, wo und wann Anzeigen in Inhalten abgespielt werden sollten, um ein reibungsloses, weniger störendes Erlebnis zu bieten, das zu Wiederholungsbesuchen führt.

* **Ganzheitliche Übersicht:** Kombinieren Sie verschiedene Datenpunkte Ihrer Inhaltsdistributorinnen und -distributoren, um eine umfassende Übersicht all Ihre Medienaktivitäten zu erhalten und die Interaktion und Aufrufe über alle Kanäle hinweg zu messen.

  Mit Streaming-Mediendiensten können Sie das vollständige Kunden-Journey auf Ihrer Site und in Streaming-Apps verfolgen, um den Kundenpfad und die Kundeninteressen zu visualisieren und erweiterte Empfehlungen bereitzustellen sowie Kundenerlebnisse zu personalisieren.  Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente kategorisieren und alle Metadaten erfassen, die Sie für eine vollständige und detaillierte Analyse benötigen. Anschließend können Sie Daten analysieren und Erfolgskriterien den vollständig genutzten Medien, der durchschnittlich verbrachten Zeit und an abgeschlossenen Anzeigen zuordnen.

* **Wichtige Metriken**: Sie können wichtige Bereitstellungsmetriken in Bezug auf die Erlebnisqualität (Quality of Experience, QoE) messen, z. B. ausgelassene Frames, Pufferzeit und durchschnittliche Bit-Rate.

* **Erhöhte Granularität**: Bewerten Sie das Ansichtsverhalten auf einer extrem detaillierten Ebene, einschließlich der Besuchszeit einzelner Benutzer, gleichzeitige Betrachter/Zuhörer nach Minuten und der durchschnittlichen Konsumdauer des Inhalts.

* **Präzise Messung**: Führen Sie Messungen auf zahlreichen für den Medienkonsum verwendeten Geräten durch, einschließlich OTT, Smartphone, Tablet, Desktop, um Interaktionsmuster und -gewohnheiten der Benutzer zu überwachen.

* **Segmentierung**: Wenden Sie Klassifizierungen auf Ihre Player, Geräte, Genres und Kapitel an und zeigen Sie, wie sich diese auf Ihre gesamten Aufrufe und Kundeninteraktionen mit Inhalten, Audio, Anzeigen und kombinierten Inhalten auswirken.


## Funktionsweise

Tracking-Daten von Streaming-Mediendiensten werden von einem Player mithilfe der Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDKs, Media Edge-API oder der Mediensammlungs-API erfasst.

Alle granularen Daten (bis zu 10 Sekunden) werden entweder an den Media Analytics-Dienst oder an Experience Edge gesendet (je nach gewählter [Implementierungsmethode](/help/implementation/overview.md)), die die Daten für jede einzelne Wiedergabesitzung erfassen und verarbeiten.

Nach dem Ende einer Wiedergabesitzung werden die berechneten Tracking-Daten zur Speicherung und zum Reporting entweder an Adobe Analytics oder an Customer Journey Analytics gesendet.

>[!NOTE]
>
>Bei Customer Journey Analytics-Implementierungen können Daten entweder über Experience Edge oder über Analytics Data Connector (ADC) an Customer Journey Analytics gesendet werden.


Detaillierte Informationen zu den verschiedenen Implementierungsmethoden finden Sie unter [Implementieren von Streaming-Mediendiensten für Adobe Analytics oder Customer Journey Analytics](/help/implementation/overview.md).
