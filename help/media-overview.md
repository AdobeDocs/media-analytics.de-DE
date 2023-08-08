---
title: Übersicht über Adobe Analytics für Streaming-Medien
description: Verwenden Sie Analytics für Streaming-Medien, um wichtige Einblicke in Inhalte, Audio und Werbung zu erhalten.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: ht
source-wordcount: '590'
ht-degree: 100%

---

# Übersicht über Adobe Analytics für Streaming-Medien

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics für Streaming-Medien bietet leistungsstarke Messwerkzeuge für Audio, Video und Werbung. Sie können Metriken von Streaming-Medien mit anderen Adobe Analytics-Funktionen wie Audience Analytics, Mobile oder geräteübergreifenden Analysen kombinieren.

Streaming-Medien können als Add-on zu Adobe Analytics erworben werden<!-- update this when SKUs are available for other AEP products --> und Streaming-Medien-Metriken lassen sich einfach in die folgenden Adobe Experience Platform-Produkte integrieren:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Wenden Sie sich zur Implementierung von Adobe Analytics für Streaming-Medien an Ihre Adobe-Kundenbetreuung oder das Adobe-Accountteam, um sicherzustellen, dass Streaming-Medien Teil Ihres Produktportfolios sind.

## Wichtigste Funktionen

Zu den Vorteilen von Adobe Analytics für Streaming-Medien zählen Echtzeitüberwachung, detaillierte Analysen, umsetzbare Erkenntnisse Monetarisierungsmöglichkeiten und mehr.

* **Echtzeit-Analyse**: Treffen Sie fundierte Entscheidungen in Echtzeit, indem Sie wichtige Leistungsmetriken wie Medienstarts kanalübergreifend verwenden.

  Mit Analytics für Streaming-Medien erhalten Sie nahezu in Echtzeit granulare Details zu Dauer, Stopps und Starts, mit denen Sie Video- und Audiometriken auswerten und kombinieren können. Diese Erkenntnisse ermöglichen es Ihnen, die Seh- und Hörgewohnheiten Ihrer Kundinnen und Kunden zu verstehen und mit hochgradig personalisierten Empfehlungen die Interaktion zu steigern.

* **Förderung der Interaktion**: Die Interaktion der Benutzenden wird gefördert, indem die Pufferung verringert wird und ermittelt wird, wo und wann Anzeigen in Inhalten abgespielt werden sollten, um ein reibungsloses, weniger störendes Erlebnis zu bieten, das zu Wiederholungsbesuchen führt.

* **Ganzheitliche Übersicht:** Kombinieren Sie verschiedene Datenpunkte Ihrer Inhaltsdistributorinnen und -distributoren, um eine umfassende Übersicht all Ihre Medienaktivitäten zu erhalten und die Interaktion und Aufrufe über alle Kanäle hinweg zu messen.

  Mit Adobe Analytics für Streaming-Medien können Sie die vollständige Journey Ihrer Kundinnen und Kunden auf Ihrer Site und Ihren Streaming-Apps verfolgen, um den Pfad und die Interessen von Kundinnen und Kunden visualisieren zu können, erweiterte Empfehlungen zu geben und Kundenerlebnisse zu personalisieren.  Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente kategorisieren und alle Metadaten erfassen, die Sie für eine vollständige und detaillierte Analyse benötigen. Anschließend können Sie Daten analysieren und Erfolgskriterien den vollständig genutzten Medien, der durchschnittlich verbrachten Zeit und an abgeschlossenen Anzeigen zuordnen.

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


Detaillierte Informationen zu den verschiedenen Implementierungsmethoden finden Sie unter [Implementieren von Streaming-Medien für Adobe Analytics oder Customer Journey Analytics](/help/implementation/overview.md).
