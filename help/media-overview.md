---
title: Übersicht über Adobe Analytics für Streaming-Medien
description: Verwenden Sie Streaming Media Analytics, um leistungsstarke Einblicke in Inhalte, Audio und Werbung zu erhalten.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 16%

---

# Übersicht über Adobe Analytics für Streaming-Medien

![Banner](./assets/media_analytics_banner.png)

Adobe Analytics für Streaming-Medien ist ein Add-on zu Adobe Analytics, das leistungsstarke Mess-Tools für Audio, Video und Werbung bietet. Mit Analytics für Streaming-Medien erhalten Sie nahezu detaillierte Echtzeitdetails zur Dauer, zu Stopps und Start, mit denen Sie Video- und Audiometriken auswerten und kombinieren können. Diese Einblicke ermöglichen es Ihnen, die Anzeige- und Listening-Gewohnheiten Ihrer Kunden zu verstehen und die Interaktion mit hochpersonalisierten Empfehlungen zu steigern.

Mit Adobe Analytics für Streaming-Medien können Sie die vollständige Journey Ihrer Kunden über Ihre Site und Streaming-Apps hinweg verfolgen. Sie können Streaming-Medien-Metriken mit anderen Adobe Analytics-Funktionen wie Audience Analytics, Mobile oder geräteübergreifende Analysen kombinieren. Die Metriken lassen sich einfach in Adobe Analytics-Berichte und andere Adobe Experience Platform-Produkte integrieren. Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente kategorisieren und alle Metadaten erfassen, die Sie für eine vollständige und detaillierte Analyse benötigen. Anschließend können Sie Daten analysieren und Erfolgskriterien den vollständig genutzten Medien, der durchschnittlich verbrachten Zeit und an abgeschlossenen Anzeigen zuordnen.

Sie können wichtige Bereitstellungsmetriken im Zusammenhang mit der Erlebnisqualität (QoE) messen, z. B. Dropped Frames, Pufferung und durchschnittliche Bitrate. Außerdem können die Metriken mit Ihren Website- oder App-Daten kombiniert werden, um den Kundenpfad und die Kundeninteressen zu visualisieren und so erweiterte Empfehlungen zu erhalten und Kundenerlebnisse mit Adobe Experience Platform zu personalisieren.

## Funktionsweise

Tracking-Daten zu Streaming-Medien werden von einem Player mit den Media SDKs, den Media Collection APIs oder den Media Extensions (mit Tags) erfasst. Alle granularen Daten (bis zu 10 Sekunden) werden an den Media Analytics-Dienst gesendet, der die Daten für jede einzelne Wiedergabesitzung erfasst und verarbeitet. Sobald eine Wiedergabesitzung beendet ist, werden die berechneten Tracking-Daten zur Speicherung und Berichterstellung an Adobe Analytics gesendet. Bei Adobe Customer Journey Analytics-Implementierungen (CJA) können Daten mithilfe des Analytics Data Connector (ADC) an CJA gesendet werden, damit Kunden CJA als Reporting-Tool verwenden können.

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="Prozess für Streaming-Medien" width="75%">
</div>

## Funktionen

Zu den Vorteilen von Adobe Analytics für Streaming-Medien zählen Echtzeit-Monitoring, detaillierte Analyse, umsetzbare Insights und Möglichkeiten der finanziellen Verwertung.

* **Echtzeitanalyse**: Treffen Sie umsetzbare Entscheidungen in Echtzeit mithilfe von wichtigen Leistungsmetriken wie Medienstarts über mehrere Kanäle hinweg.

* **Förderung der Interaktion**: Die Interaktion mit den Benutzern wird gefördert, indem die Pufferung verringert wird und ermittelt wird, wo und wann Anzeigen in Inhalten abgespielt werden sollten, um ein reibungsloses, weniger störendes Erlebnis zu bieten, das Wiederholungsbesuche ermöglicht.

* **Ganzheitliches Bild**: Kombinieren Sie mehrere Datenpunkte Ihrer Inhaltsdistributoren, um eine umfassende Übersicht über all Ihre Medienaktivitäten zu erhalten. Mit der Federated Analytics-Funktion können Sie die Interaktion und Aufrufe über alle Kanäle hinweg messen.

* **Erhöhte Granularität**: Bewerten Sie das Anzeigeverhalten auf der detailliertesten Ebene, einschließlich der individuellen Besucherzeit, gleichzeitigen Betrachtern oder Zuhörern nach Minuten und der durchschnittlichen Konsumdauer des Inhalts.

* **Präzise Messung**: Messen Sie die verschiedenen für den Medienkonsum verwendeten Geräte, einschließlich OTT, Smartphone, Tablet, Desktop und mehr, um Interaktionsmuster und -gewohnheiten der Benutzer zu überwachen.

* **Segmentierung**: Wenden Sie Klassifizierungen auf Ihre Player, Geräte, Genres, Kapitel und Anzeigen an, um zu sehen, wie sich diese auf Ihre gesamten Ansichten/Aufrufe und Kundeninteraktionen mit Inhalten, Audio, Anzeigen und kombinierten Inhalten auswirken.
