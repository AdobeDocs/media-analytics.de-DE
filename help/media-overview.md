---
title: Messen von Audio und Video in Adobe Analytics
description: Adobe Analytics for Media (auch als Media Analytics bezeichnet) bietet Clients eine robuste Medienmessung für Inhalte, Audio und Werbung.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Messen von Audio und Video in Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Info zu Adobe Analytics für Audio und Video

Adobe Analytics für Audio und Video ist ein Add-on zu Adobe Analytics, das leistungsstarke Messwerkzeuge für Audio, Video und Werbung bietet. Adobe Analytics ist Teil der Adobe Experience Platform.

Mit Adobe Analytics für Audio und Video können Sie die gesamte Customer Journey auf Ihrer Site verfolgen. Die Metriken lassen sich problemlos in Adobe Analytics-Berichte und andere Adobe Experience Cloud-Produkte integrieren. Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente kategorisieren und alle Metadaten erfassen, die Sie für eine vollständige und detaillierte Analyse benötigen. Anschließend können Sie Daten analysieren und Erfolgskriterien voll genutzten Medien, durchschnittlich verbrachter Zeit und abgeschlossene Anzeigen zuordnen.

Sie können wichtige QoS-Metriken zum Versand messen, z. B. Dropped Frames, die Besuchszeit für Pufferung und die durchschnittliche Bitrate. Außerdem können die Metriken mit Ihren Website- oder App-Daten kombiniert werden, um den Kundenpfad und die Kundeninteressen zu visualisieren, um erweiterte Empfehlungen zu erhalten und Kundenerlebnisse mithilfe der Adobe Experience Cloud zu personalisieren.

## Funktionen {#features}

Zu den Vorteilen von Adobe Analytics für Audio und Video zählen Echtzeitüberwachung, detaillierte Analyse, umsetzbare Einblicke und Monetarisierungsmöglichkeiten.
* **Echtzeit-Analyse**- Treffen Sie umsetzbare Entscheidungen in Echtzeit, indem Sie wichtige Leistungsmetriken wie &quot;duration&quot;, &quot;ex2&quot;und &quot;ex3&quot;für mehrere Kanal verwenden. Hauptinhaltereignisse werden in 10-Sekunden-Intervallen gemessen, um Aktivitäten zu erfassen, sobald sie auftreten. EAnzeigen-Tracking-Ereignisse treten in Intervallen von 1 Sekunde auf.
* **Interaktion** fördern - Nutzen Sie die Vorteile von weniger Pufferung-Ereignissen, um zu verstehen, wo und wann Anzeigen innerhalb des Inhalts abgespielt werden sollten, um eine reibungslose und weniger störende Funktion zu gewährleisten, die wiederholte Besuche ermöglicht.
* **Ganzheitliches Bild**- Kombinieren Sie mehrere Datenpunkte über all Ihre Content-Distributoren hinweg, um eine vollständige Ansicht Ihrer gesamten Aktivität zu erhalten. Messen Sie mithilfe der Federated Analytics-Funktion Interaktionen und Ansichten/Listening über alle möglichen Kanal hinweg.
* **Erhöhte Granularität**- Bewerten Sie das Ansichtsverhalten auf der granulärsten Ebene, einschließlich der individuellen Tageszeit des Besuchers, gleichzeitiger Viewer/Listener nach Minuten und der durchschnittlichen Nutzungsdauer des Inhalts.
* **Präzise Messung**- Messen Sie die verschiedenen Geräte, die für den Medienkonsum verwendet werden, einschließlich OTT, Smartphone, Tablet, Desktop und mehr, um Interaktionsmuster und -gewohnheiten der Benutzer zu überwachen.
* **Segmentierung**: Wenden Sie Klassifizierungen auf Ihre Player, Geräte, Genres und Kapitel an und zeigen Sie, wie sich diese auf Ihre Ansichten/Listening-Aktivitäten insgesamt auswirken und die Kundeninteraktion mit Inhalten, Audio, Anzeigen und kombinierten Inhalten.

## Heartbeat-Messung {#heartbeat}

Adobe Analytics verwendet &quot;Heartbeats&quot;, um Videometriken zu erfassen. Während der Videowiedergabe werden Heartbeats an den Heartbeat-Tracking-Server gesendet, um die Wiedergabedauer zu messen. Die Heartbeat-Aufrufe werden alle zehn Sekunden gesendet. Heartbeats führen zu granularen Videonutzungsmetriken und präziseren Video-Fallout-Berichten. Adobe Analytics für Audio und Video misst Heartbeats mit Adobe Launch mit der Media Analytics-Erweiterung, dem Media SDK und der Media Collection-API. Die `AppMeasurement` und `VisitorID` Komponenten werden zum Empfangen von Videodaten verwendet.

Die Verwendung von Heartbeats in Adobe Analytics für Audio und Video bietet folgende Vorteile:

| Funktion | Beschreibung |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Media-Ereignisse | Detaillierte und benutzerdefinierte Ereignis werden alle 10 Sekunden für Hauptinhalte und alle 1 Sekunde für Anzeigen gesendet |
| Metriken und Dimensionen | Klare standardisierte Metriken, Dimensionen und Benchmarks für alle<br>AnbieterMit einer standardisierten Lösung für alle Plattformen können Sie konsistente, standardisierte Variablen für alle Medien und Plattformen verwenden, um einen effizienteren Vergleich zwischen Kampagne, Geräten und Anbietern zu ermöglichen. |
| Integrationen | Experience Cloud ID ist mit der Adobe Experience Cloud verknüpft, um eine benutzerübergreifende<br>Analyse zu erleichtern. Dank der automatischen Adobe Experience Cloud-Integration können Sie Ihre Mediendateien segmentieren, Zielgruppen vornehmen und Medienempfehlungen basierend auf den Benutzereinstellungen abgeben. |
| Preise  | Transparentes Tracking jedes Medienstreams (einzeln) |
| Implementierung und Support | Optimierte Konfiguration mit fortlaufenden Aktualisierungen und<br>VerbesserungenMit einem optimierten Implementierungsprozess können Sie schnell Variablen über Ihre Player-API zuordnen und Implementierungen mit dem Adobe Debug Tool validieren, um sicherzustellen, dass alle erforderlichen Variablen genau verfolgt werden. |
| Partnerfreigabe | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| Erweitertes Tracking | Download-Content-Verfolgung, Fehlerwiederherstellungsverfolgung und gleichzeitige<br>ViewerSie können Audio- und Videoinhalte verfolgen, die auf ein Gerät heruntergeladen und wiedergegeben werden, unabhängig von dessen Konnektivität. |



## Sicherheit {#security}

Bei Adobe nehmen wir die Sicherheit Ihrer digitalen Assets ernst. Von der konsequenten Integration von Sicherheit in unseren internen Softwareentwicklungsprozess und unsere Tools bis hin zu unseren funktionsübergreifenden Incident Response Teams streben wir danach, proaktiv und imimposant zu sein. Darüber hinaus hilft uns unsere Zusammenarbeit mit Partnern, Forschern und anderen Branchenverbänden dabei, die neuesten Bedrohungen und Best Practices für die Sicherheit zu verstehen und die Sicherheit unserer Angebote kontinuierlich zu erhöhen.


### Transport Layer Security {#transport-layer-security}

**TLS-Hinweis:** Aufgrund der Sicherheitsstandards von Adobe müssen ältere Sicherheitsprotokolle durch neue ersetzt werden. Um die sich weiterentwickelnden Standards für Sicherheitsprotokolle weiterhin zu erfüllen, setzt Adobe auf TLS 1.2, um die aktuelle und sicherste Version zu verwenden. Ab dem 20. Februar 2019 unterstützt Adobe nur TLS 1.1 oder höher. Mit dieser Änderung erfasst Adobe keine Daten mehr von Endbenutzern mit älteren Geräten oder Webbrowsern, die TLS 1.0 bereitstellen. Die Migration auf TLS 1.2 bietet eine verbesserte Sicherheit. Für einen reibungslosen Übergang sollten Sie die Details zu diesem Thema genau durchlesen und die Änderungen entsprechend planen.

>[!NOTE]
>
>TLS ist derzeit das am weitesten verbreitete Sicherheitsprotokoll, das in Webbrowsern und anderen Anwendungen Verwendung findet, bei denen über ein Netzwerk übertragene Daten geschützt werden müssen.
