---
title: Messen von Dampfmedien in Adobe Analytics
description: Adobe Analytics for Media (auch als Media Analytics bezeichnet) bietet Clients eine robuste Medienmessung für Inhalte, Audio und Werbung.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: fdec4da99a43d889690638f1ff3579e145548b69
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 85%

---


# Messen von Dampfmedien in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Info zu Adobe Analytics für Streaming Media

Adobe Analytics for Streaming Media ist ein Add-on zu Adobe Analytics, das leistungsstarke Messwerkzeuge für Audio, Video und Werbung bietet. Adobe Analytics ist Teil der Adobe Experience Platform.

Mit Adobe Analytics for Streaming Media können Sie die gesamte Customer Journey auf Ihrer Site verfolgen. Die Metriken lassen sich problemlos in Adobe Analytics-Berichte und andere Adobe Experience Cloud-Produkte integrieren. Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente kategorisieren und alle Metadaten erfassen, die Sie für eine vollständige und detaillierte Analyse benötigen. Anschließend können Sie Daten analysieren und Erfolgskriterien den vollständig genutzten Medien, der durchschnittlich verbrachten Zeit und an abgeschlossenen Anzeigen zuordnen.

Sie können wichtige QoS-Metriken messen, wie z. B. Dropped Frames, Pufferung und durchschnittliche Bitrate. Außerdem können die Metriken mit Ihren Website- oder App-Daten kombiniert werden, um den Kundenpfad und die Kundeninteressen zu visualisieren. So können erweiterte Empfehlungen bereitgestellt und Kundenerlebnisse mithilfe der Adobe Experience Cloud personalisiert werden.

## Funktionen {#features}

Zu den Vorteilen von Adobe Analytics für Streaming Media zählen Echtzeitüberwachung, detaillierte Analyse, umsetzbare Einblicke und Monetarisierungsmöglichkeiten.
* **Echtzeit-Analyse**- Treffen Sie umsetzbare Entscheidungen in Echtzeit, indem Sie wichtige Leistungsmetriken wie „Dauer“, „ex2“ und „ex3“ für mehrere Kanäle verwenden. Hauptinhaltereignisse werden in zehn-Sekunden-Intervallen gemessen, um Aktivitäten zu erfassen, sobald sie auftreten. Anzeigen-Tracking-Ereignisse treten in Intervallen von einer Sekunde auf.
* **Förderung der Interaktion** - Die Interaktion der Benutzer wird gefördert, indem die Pufferung verringert wird und ermittelt wird, wo und wann Anzeigen in Inhalten abgespielt werden sollten, um ein reibungsloses, weniger störendes Erlebnis zu bieten, das zu Wiederholungsbesuchen führt.
* **Ganzheitliche Übersicht** - Kombinieren Sie verschiedene Datenpunkte Ihrer Inhaltsdistributoren, um eine umfassende Übersicht aller Medienaktivitäten zu erhalten. Mit Federated Analytics können Sie die Interaktion und Aufrufe auf allen Kanälen messen.
* **Erhöhte Granularität** - Bewerten Sie das Ansichtsverhalten auf einer extrem detaillierten Ebene, einschließlich der Besuchszeit einzelner Benutzer, gleichzeitige Betrachter/Zuhörer nach Minuten und der durchschnittlichen Konsumdauer des Inhalts.
* **Präzise Messung** - Führen Sie Messungen auf zahlreichen für den Medienkonsum verwendeten Geräten durch, einschließlich OTT, Smartphone, Tablet, Desktop, um Interaktionsmuster und -gewohnheiten der Benutzer zu überwachen.
* **Segmentierung** - Wenden Sie Classifications auf Ihre Player, Geräte, Genres und Kapitel an und zeigen Sie, wie sich diese auf Ihre gesamten Aufrufe und Kundeninteraktionen mit Inhalten, Audio, Anzeigen und kombinierten Inhalten auswirken.

## Heartbeat-Messung {#heartbeat}

Adobe Analytics verwendet „Heartbeats“, um Videometriken zu erfassen. Während der Videowiedergabe werden Heartbeats an den Heartbeat-Tracking-Server gesendet, um die Wiedergabedauer zu messen. Die Heartbeat-Aufrufe werden alle zehn Sekunden gesendet. Heartbeats führen zu granularen Videointeraktionsmetriken und präziseren Video-Fallout-Berichten. Adobe Analytics for Streaming Media misst Heartbeats mit Adobe Launch mit der Media Analytics-Erweiterung, dem Media SDK und der Media Collection-API. Die Komponenten `AppMeasurement` und `VisitorID` werden zum Empfangen von Videodaten verwendet.

Die Verwendung von Heartbeats Adobe Analytics für Streaming Media bietet folgende Vorteile:

| Funktion | Beschreibung |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medienereignisse | Detaillierte und benutzerdefinierte Ereignisse werden alle zehn Sekunden für Hauptinhalte und jede Sekunde für Anzeigen gesendet. |
| Metriken und Dimensionen | Klare, standardisierte Metriken, Dimensionen und Benchmarks für alle Anbieter<br>Mit einer standardisierten Lösung für alle Plattformen können Sie konsistente, standardisierte Variablen für alle Medien und Plattformen verwenden, um einen effizienteren Vergleich zwischen Kampagnen, Geräten und Anbietern zu ermöglichen. |
| Integrationen | Experience Cloud ID ist mit Adobe Experience Cloud verknüpft, um eine benutzerübergreifende<br>Analyse zu erleichtern. Dank der automatischen Adobe Experience Cloud-Integration können Sie Ihre Medien-Zielgruppen segmentieren, Zielgruppen auswählen und Medienempfehlungen basierend auf den Benutzereinstellungen bereitstellen. |
| Preise | Transparentes Tracking jedes Medien-Streams (einzeln) |
| Implementierung und Support | Optimierte Konfiguration mit fortlaufenden Aktualisierungen und Verbesserungen<br>Mit einem optimierten Implementierungsprozess können Sie schnell Variablen über Ihre Player-API zuordnen und Implementierungen mit dem Adobe Debug Tool validieren, um sicherzustellen, dass alle erforderlichen Variablen präzise getrackt werden. |
| Partnerfreigabe | Federated Analytics und Certified Metrics<br>Mit freigegebenen Daten über Federated Analytics können Sie unsere branchenführenden Medien-Sharing-Funktionen nutzen, um die Daten aller Medienverteilungspartner – Betreiber, Programmierer und Distributoren – ganzheitlich zu evaluieren. |
| Erweitertes Tracking | Verfolgung von heruntergeladenen Inhalten, Fehlerwiederherstellung und gleichzeitige Viewer<br>Sie können Streaming-Medieninhalte verfolgen, die auf ein Gerät heruntergeladen und wiedergegeben werden, unabhängig von dessen Konnektivität. |



## Sicherheit {#security}

Wir von Adobe nehmen die Sicherheit Ihrer digitalen Assets sehr ernst. Von der konsequenten Integration von Sicherheit in unseren internen Softwareentwicklungsprozess über unsere Tools bis hin zu unseren funktionsübergreifenden Incident Response Teams streben wir danach, proaktiv und agil zu sein. Darüber hinaus hilft uns unsere Zusammenarbeit mit Partnern, Forschern und anderen Branchenverbänden dabei, die neuesten Bedrohungen und Best Practices für die Sicherheit zu verstehen und die Sicherheit unserer Produkte und Dienste kontinuierlich zu erhöhen.


### Transport Layer Security {#transport-layer-security}

**TLS-Hinweis:** Aufgrund der Sicherheitsstandards von Adobe müssen ältere Sicherheitsprotokolle durch neue ersetzt werden. Um die sich weiterentwickelnden Standards für Sicherheitsprotokolle weiterhin zu erfüllen, setzt Adobe auf TLS 1.2, um die aktuelle und sicherste Version zu verwenden. Ab dem 20. Februar 2019 unterstützt Adobe nur TLS 1.1 oder höher. Mit dieser Änderung erfasst Adobe keine Daten mehr von Endbenutzern mit älteren Geräten oder Webbrowsern, die TLS 1.0 bereitstellen. Die Migration auf TLS 1.2 bietet eine verbesserte Sicherheit. Für einen reibungslosen Übergang sollten Sie die Details zu diesem Thema genau durchlesen und die Änderungen entsprechend planen.

>[!NOTE]
>
>TLS ist derzeit das am weitesten verbreitete Sicherheitsprotokoll, das in Webbrowsern und anderen Anwendungen Verwendung findet, bei denen über ein Netzwerk übertragene Daten geschützt werden müssen.
