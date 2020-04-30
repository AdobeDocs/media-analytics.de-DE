---
title: Messen von Audio und Video in Adobe Analytics
description: 'Adobe Analytics for Media (auch als Media Analytics bezeichnet) bietet Clients eine robuste Medienmessung für Inhalte, Audio und Werbung. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Messen von Audio und Video in Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>Die hier bereitgestellte Dokumentation gilt für Clients mit Version 1.5 (oder höher) des *Media SDK* bzw. der neuen *Media Collection API* von Adobe für Heartbeat-Messungen. Sie enthält keine Anweisungen zur veralteten Videoimplementierung mit Meilensteinen. Wir empfehlen allen Kunden, zu einer oder beiden der zwei neuesten Medien-Tracking-Lösungen zu wechseln, um von Verbesserungen und erweiterten Messungen zu profitieren. Unten finden Sie die [Vorteile, die der Umstieg auf die neuesten Lösungen](media-overview.md#heartbeat-versus-milestone-benefits), bietet. Zwar werden wir die Meilensteinmethode zum Video-Tracking weiterhin unterstützen, jedoch sind hier keine Updates, Fixes oder künftigen Verbesserungen geplant. Wenden Sie sich an Ihren Adobe-Account-Manager, wenn Sie weitere Fragen haben.

## Überblick {#overview}

Adobe Analytics for Media (auch als Media Analytics bezeichnet) ist ein Add-on zum Analytics-Basisangebot, durch das Kunden eine umfassende Medienmessung für Inhalte, Audio und Werbung durchführen können. Media Analytics bietet Kunden zahlreiche Vorteile. Sie können damit Echtzeitüberwachung, detaillierte Analysen, hilfreiche Einblicke und Monetarisierungsmöglichkeiten nutzen.

Das Medien-Tracking wird durch eines der folgenden Tools aktiviert:

* **Media SDK -** Integration mit den am häufigsten verwendeten Medienplayern.
* **Mediensammlungs-API -** (RESTful API) Integration mit Playern, für die es kein unterstütztes SDK gibt (oder mit Playern, für die keine SDK-Integration gewünscht wird).

Mit Adobe Analytics for Media können Kunden die gesamte Customer Journey ihrer Website verfolgen, wozu auch der Medienkonsum gehört. Diese Messungen lassen sich problemlos in Analytics-Berichte und andere Experience Cloud-Produkte integrieren. Mit der Medienmessung können Sie Ihre Daten in mehrere Dimensionen und Segmente unterteilen und damit alle Metadaten erfassen, die Sie benötigen, um eine detaillierte Analyse durchzuführen und eine Zuordnung von Erfolgskriterien zu vollständig genutzten Medien, der durchschnittlichen Besuchszeit und den bis zum Ende betrachteten Anzeigen durchzuführen.

Die Medienlösungen messen nicht nur wichtige QoS-Metriken, wie z. B. Dropped Frames, Pufferung und durchschnittliche Bitrate. Die Lösungen können auch mit Ihren Website- oder App-Daten kombiniert werden, um den Fluss der Kunden und deren Interessen zu visualisieren. Damit lassen sich dann besser Empfehlungen senden und Erlebnisse mit Hilfe von Adobe Experience Cloud personalisieren.

## Vorteile {#benefits}

Zu den zahlreichen Vorteilen, die die Medienmesslösungen von Adobe bieten, zählen:

* **Schnelle Analyse -** Treffen Sie Entscheidungen anhand von aussagekräftigen Echtzeitmetriken zur Performance (z. B. Dauer) über verschiedene Kanäle hinweg. Hauptinhaltereignisse werden in **10-Sekunden**-Intervallen gemessen, um Aktivitäten zu erfassen, sobald sie auftreten. EAnzeigen-Tracking-Ereignisse treten in Intervallen von **1 Sekunde** auf.
* **Förderung der Interaktion -** Die Interaktion der Benutzer wird gefördert, indem die Pufferung verringert wird und ermittelt wird, wo und wann Anzeigen in Inhalten abgespielt werden sollten, um ein reibungsloses, weniger störendes Erlebnis zu bieten, sodass Benutzer Ihre Site gern wieder besuchen.
* **Ganzheitliche Übersicht -** Kombinieren Sie verschiedene Datenpunkte Ihrer Inhaltsdistributoren, um eine umfassende Übersicht aller Medienaktivitäten zu erhalten und die Interaktion und Aufrufe mit [Federated Analytics](/help/federated-analytics.md) über alle Kanäle hinweg zu messen.
* **Erhöhte Granularität -** Bewerten Sie das Ansichtsverhalten auf einer extrem detaillierten Ebene, einschließlich der Besuchszeit einzelner Benutzer, gleichzeitige Betrachter/Zuhörer nach Minuten und der durchschnittlichen Konsumdauer des Inhalts.
* **Präzise Messung -** Führen Sie Messungen auf zahlreichen für den Medienkonsum verwendeten Geräten durch, einschließlich OTT, Smartphone, Tablet, Desktop, um Interaktionsmuster und -gewohnheiten der Benutzer zu überwachen.
* **Segmentierung -** Wenden Sie Klassifizierungen auf Ihre Player, Geräte, Genres und Kapitel an und zeigen Sie, wie sich diese auf Ihre gesamten Aufrufe und Kundeninteraktionen mit Inhalten, Audio, Anzeigen und kombinierten Inhalten auswirken.

## Vorteile von Heartbeat gegenüber Milestone {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media kann die Messung auf zwei Arten durchführen: über die veraltete Meilensteinmethode (nur Video) oder die aktuelle Heartbeat-Methode (Audio und Video, im Media SDK und der Media Collection API enthalten). Die Heartbeats-Methode ist die bevorzugte Messmethode. Wir empfehlen allen Kunden, zu dieser Version zu wechseln, falls sie dies noch nicht getan haben, um die unten beschriebenen Vorteile nutzen zu können.

Die Legacy-Meilensteinmethode basiert auf individuellen Server-Aufrufen an den Analytics-Server für Videostarts, für Quartilen, für die Dauer und für Beendigungen. Die Heartbeats-Methode bietet eine umfassendere Medien-Tracking-Lösung, die Hauptinhalte in 10-Sekunden-Intervallen misst und dadurch erweiterte, standardisierte Metriken liefert. Darüber hinaus hat Adobe von der Meilensteinmethode gelernt und stellt jetzt einen reibungsloseren, optimierten Implementierungsprozess über die von Heartbeats verwendete Media SDK- oder Media Collection-API bereit.

Zu den zahlreichen Vorteilen der Heartbeats-Methode zählen:

* **Optimierter Implementierungsprozess -** Mit der Player-API lassen sich Variablen einfacher zuordnen und Implementierungen mit dem Adobe Debug Tool validieren, um sicherzustellen, dass alle erforderlichen Variablen korrekt getrackt werden.
* **Automatische Adobe Experience Cloud-Integration-** Nutzen Sie die automatische Integration in die Adobe Experience Cloud mithilfe der Experience Cloud ID, segmentieren Sie Ihre Medienzielgruppen, sprechen Sie sie gezielt an und stellen Sie basierend auf Anwendervorlieben Medienempfehlungen bereit.
* **Freigegebene Daten über Federated Analytics -** Nutzen Sie unsere branchenführenden Medien-Sharing-Funktionen, um die Daten aller Medienverteilungspartner – Betreiber, Programmierer und Distributoren – ganzheitlich zu evaluieren.
* **Standardisierte Lösung für alle Plattformen -** Nutzen Sie über alle Medienplattformen hinweg einheitliche und standardisierte Variablen, um effizientere Vergleiche zwischen Kampagnen, Geräten und Anbietern zu ermöglichen.
* **Tracking heruntergeladener Inhalte -** Tracking von Medieninhalten (Video und Audio), die unabhängig von der Internetverbindung heruntergeladen und über ein Gerät abgespielt werden.

### Vergleichstabelle

|  | Video Analytics – Milestone | Media Analytics – Heartbeats |
|---|---|---|
| **Media-Ereignisse** | Wichtige Standard-Ereignisse | Detaillierte benutzerspezifische Ereignisse alle zehn Sekunden für Hauptinhalte, jede Sekunde für Anzeigen |
| **Metriken und Dimensionen** | Unterschiede zwischen Anbietern, Metriken und Dimensionen sind nicht standardisiert | Klare, standardisierte Metriken, Dimensionen und Benchmarks bei allen Anbietern |
| **Integration mit Adobe-Produkten** | Einzelne Sitzungen mit einigen Zuordnungen und Integrationen | Für eine einfachere Analyse wurde die Adobe Experience Cloud-ID mit der gesamten Adobe Experience Cloud verknüpft. |
| **Preise** | Getrackt und mit jedem Server-Aufruf in Rechnung gestellt | Transparentes Tracking jedes Medienstreams (einzeln) |
| **Implementierung und Support** | Längere Integrationen mit eingeschränkter Unterstützung älterer Versionen und ohne Upgrades | Optimierte Konfiguration mit laufenden Aktualisierungen und Verbesserungen |
| **Partnerfreigabe** | nicht angegeben | Federated Analytics und zertifizierte Metriken |
| **Erweitertes Tracking** | nicht angegeben | Tracking der Fehlerwiederherstellung und der gleichzeitigen Betrachter |

## Unterstützte Geräte {#devices-supported}

Adobe Analytics for Media hat sich mit der Branche weiterentwickelt und stellt leistungsstarke Datenerfassungs-Tools bereit, mit denen sichergestellt wird, dass jeder Medienstream auf allen wichtigen Geräten erfasst wird und in Berichte aufgenommen wird. Unser Media SDK wurde für die am häufigsten verwendeten Geräte entwickelt, darunter:

* iOS- und Android-Smartphones und -Tablets
* OTT-Geräte für ROKU, AppleTV, FireTV und Android-TV
* JavaScript-Browser für Desktop und Laptop

Die SDKs werden routinemäßig aktualisiert, wenn neue Versionen von Geräten veröffentlicht werden. Sie können diese SDKs verwenden, um eine Integration mit dem Großteil der heutigen Medienplayer herzustellen, einschließlich Brightcove und Ooyala.

Für Geräte oder Plattformen, die derzeit keine SDK-Unterstützung haben (oder doch haben), können Sie die Mediensammlungs-API implementieren, mit der Sie RESTful-API-Aufrufe direkt vom Gerät/der Plattform zum Media Analytics-Backend durchführen.

Die folgende Tabelle enthält eine Liste der Geräte, die derzeit durch die Implementierung unseres Media SDK und unserer Mediensammlungs-API unterstützt werden. Hier können Sie die neueste Version des SDK herunterladen: [SDKs herunterladen.](sdk-implement/download-sdks.md) Wenn ein Gerät nicht aufgeführt ist, das Sie messen möchten, erfragen Sie den Gerätestatus beim Kundendienst oder bei Ihrem Lösungsberater.

|      | Medien-SDK | Mediensammlungs-API |
|---|:---:|:---:|
| **JavaScript-Browser** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS-Geräte** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-Geräte** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Unified Windows Platforms (UWP)** |  | ![](assets/icon-blue-check.png) |
| **BlackBerry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (neu/veraltet)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Roku (JavaScript)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Roku (native App)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **FireTV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(Andere/neue vernetzte Geräte)** |  | ![](assets/icon-blue-check.png) |

Weitere Informationen zum Media SDK finden unter [Unterstützte Mindestversionen der Plattformen](./sdk-implement/setup/setup-overview.md#minimum-platform-version).

## Transport Layer Security {#transport-layer-security}

**TLS-Hinweis:** Aufgrund der Sicherheitsstandards von Adobe müssen ältere Sicherheitsprotokolle durch neue ersetzt werden. Um die sich weiterentwickelnden Standards für Sicherheitsprotokolle weiterhin zu erfüllen, setzt Adobe auf TLS 1.2, um die aktuelle und sicherste Version zu verwenden. Ab dem 20. Februar 2019 unterstützt Adobe nur TLS 1.1 oder höher. Mit dieser Änderung erfasst Adobe keine Daten mehr von Endbenutzern mit älteren Geräten oder Webbrowsern, die TLS 1.0 bereitstellen. Die Migration auf TLS 1.2 bietet eine verbesserte Sicherheit. Für einen reibungslosen Übergang sollten Sie die Details zu diesem Thema genau durchlesen und die Änderungen entsprechend planen.

>[!NOTE]
>
>TLS ist derzeit das am weitesten verbreitete Sicherheitsprotokoll, das in Webbrowsern und anderen Anwendungen Verwendung findet, bei denen über ein Netzwerk übertragene Daten geschützt werden müssen.

