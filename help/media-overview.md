---
title: Übersicht über das Adobe Streaming Media Collection Add-on
description: Verwenden Sie das Streaming-Mediensammlungs-Add-on, um leistungsstarke Einblicke in Inhalte, Audio und Werbung zu erhalten.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 64%

---

# Übersicht über das Adobe Streaming Media Collection Add-on

![Banner](./assets/media_analytics_banner.png)

Das Adobe Streaming Media Collection Add-on bietet leistungsstarke Sammlungs-, Mess- und Personalisierungswerkzeuge für Streaming-Medieninhalte wie Audio, Video und Werbung für Streaming-Medienanbieter. Sie können Streaming-Medien-Metriken mit Funktionen wie Audience Analytics, Mobile oder geräteübergreifende Analysen kombinieren.

Streaming-Mediendaten lassen sich einfach in die folgenden Adobe Experience Platform-Produkte integrieren:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Wenden Sie sich zur Implementierung der Streaming-Mediensammlung an Ihren Adobe Sales-Support-Mitarbeiter oder Adobe-Account-Team, um sicherzustellen, dass das Streaming Media Collection Add-on Teil Ihres Produktportfolios ist.

## Wichtigste Funktionen

Zu den Vorteilen des Streaming Media Collection Add-ons gehören Echtzeitüberwachung, detaillierte Analyse, umsetzbare Einblicke, Monetarisierungsmöglichkeiten und mehr.

* **Echtzeit-Analyse**: Treffen Sie fundierte Entscheidungen in Echtzeit, indem Sie wichtige Leistungsmetriken wie Medienstarts kanalübergreifend verwenden.

  Mit dem Streaming-Mediensammlungs-Add-on erhalten Sie nahezu detaillierte Echtzeitdetails zur Dauer, zu Stopps und Starts, mit denen Sie Video- und Audiometriken auswerten und kombinieren können. Diese Erkenntnisse ermöglichen es Ihnen, die Seh- und Hörgewohnheiten Ihrer Kundinnen und Kunden zu verstehen und mit hochgradig personalisierten Empfehlungen die Interaktion zu steigern.

* **Förderung der Interaktion**: Die Interaktion der Benutzenden wird gefördert, indem die Pufferung verringert wird und ermittelt wird, wo und wann Anzeigen in Inhalten abgespielt werden sollten, um ein reibungsloses, weniger störendes Erlebnis zu bieten, das zu Wiederholungsbesuchen führt.

* **Ganzheitliche Übersicht:** Kombinieren Sie verschiedene Datenpunkte Ihrer Inhaltsdistributorinnen und -distributoren, um eine umfassende Übersicht all Ihre Medienaktivitäten zu erhalten und die Interaktion und Aufrufe über alle Kanäle hinweg zu messen.

  Mit dem Streaming-Mediensammlungs-Add-on können Sie die vollständige Journey Ihrer Kunden auf Ihrer Site und in Streaming-Apps verfolgen, um den Kundenpfad und die Kundeninteressen zu visualisieren und erweiterte Empfehlungen bereitzustellen und Kundenerlebnisse zu personalisieren.  Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente kategorisieren und alle Metadaten erfassen, die Sie für eine vollständige und detaillierte Analyse benötigen. Anschließend können Sie Daten analysieren und Erfolgskriterien den vollständig genutzten Medien, der durchschnittlich verbrachten Zeit und an abgeschlossenen Anzeigen zuordnen.

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


Detaillierte Informationen zu den verschiedenen Implementierungsmethoden finden Sie unter [Implementieren des Streaming-Mediensammlungs-Add-ons für Adobe Analytics oder Customer Journey Analytics](/help/implementation/overview.md).
