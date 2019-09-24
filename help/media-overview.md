---
seo-title: Messen von Audio und Video in Adobe Analytics
title: Messen von Audio und Video in Adobe Analytics
uuid: b3cbe240-b94d-42b8-a99c-0280334aa14
translation-type: tm+mt
source-git-commit: 9b6e61e8d97ca44772f5dc2e31472a4f6c54e29c

---


# Messen von Audio und Video in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. Es enthält keine Anweisungen zur alten Milestone-Videoimplementierung. Wir empfehlen Kunden, eine der beiden aktuellen Medien-Tracking-Lösungen zu verwenden, um die Verbesserungen und die erweiterte Messung nutzen zu können. Die [Vorteile der neuen Lösungen](media-overview.md#section_cnj_5st_p1b) werden unten beschrieben. Während wir weiterhin die Meilensteinmethode zum Verfolgen von Videos unterstützen, sind keine geplanten Aktualisierungen, Fehlerbehebungen oder Verbesserungen der Funktionen geplant. Wenden Sie sich an Ihren Adobe-Account-Manager, wenn Sie weitere Fragen haben.

## Überblick {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

Adobe Analytics for Media (auch als Media Analytics bezeichnet) ist ein Add-on zum Basis-Analytics-Angebot, das Kunden eine robuste Medienmessung für Inhalte, Audio und Werbung liefert. Media Analytics bietet Kunden viele Vorteile, z. B. Echtzeitüberwachung, detaillierte Analysen, aussagekräftige Einblicke und Monetarisierungsmöglichkeiten.

Das Medien-Tracking wird durch eines der folgenden Elemente ermöglicht:

* **Medien-SDK:** Integriert mit den am häufigsten verwendeten Medienplayern.
* **Mediensammlungs-API -** (RESTful API) Integriert mit Playern, für die es keine SDK-Unterstützung gibt (oder mit Playern, für die keine SDK-Integration gewünscht wird).

   Die Mediensammlungs-API bietet zudem eine weitere Funktion, die im SDK noch nicht verfügbar ist:

   * **Tracking heruntergeladener Inhalte:** Unterstützt das Tracking von Medieninhalten (Video und Audio), die unabhängig von der Internetverbindung heruntergeladen und über ein Gerät abgespielt werden. Diese Fähigkeit basiert auf der Mediensammlungs-API und befolgt dieselbe Spezifikation für das Tracking von Abspielgeräten. (Derzeit werden keine SDKs unterstützt.)

Mit Adobe Analytics for Media können Kunden die gesamte Customer Journey über ihre Site hinweg verfolgen, einschließlich der Mediennutzung, und diese Messungen einfach in Analytics-Berichte und andere Experience Cloud-Produkte integrieren. Die Medienmessung ermöglicht die Unterteilung der Daten nach verschiedenen Dimensionen und Segmenten und erfasst alle Metadaten, die Sie für eine ausführliche Analyse sowie für die Zuordnung von Erfolgskriterien für komplett wiedergegebene Medien, durchschnittliche Besuchszeiten und abgeschlossene Anzeigen benötigen.

Die Medienlösungen messen nicht nur wichtige Lieferkennzahlen im Zusammenhang mit QoS, wie z. B. abgebrochene Frames, Zeitaufwand für die Pufferung und durchschnittliche Bitrate. Sie können auch mit Ihren Website- oder App-Daten kombiniert werden, um den Kundenverkehr und die Kundeninteressen zu visualisieren, um Empfehlungen aussprechen und um Erlebnisse über die Adobe Experience Cloud personalisieren zu können.

## Vorteile {#section_7712BA90EAE64C118218D1C581EF68B7}

Zu den Vorteilen der Adobe-Medienmessungslösungen zählen folgende Punkte:

* **Schnelle Analyse:** Treffen Sie Entscheidungen anhand von aussagekräftigen Echtzeitmetriken zur Performance (z. B. Dauer) über verschiedene Kanäle hinweg. Hauptinhaltereignisse werden in **10-Sekunden**-Intervallen gemessen, um Aktivitäten zu erfassen, sobald sie auftreten. Ereignisse zum Anzeigen-Tracking treten in **1-Sekunden**-Intervallen auf.
* **Gesteigerte Interaktion:** Binden Sie die Anwender durch weniger Pufferereignisse und durch das Verständnis, wo und wann Anzeigen innerhalb der Inhalte abgespielt werden sollten, ein, um ein reibungsloses, weniger störendes Erlebnis zu bieten, das die Anwender zur Rückkehr bewegt und wiederholte Besuche fördert.
* **Ganzheitliches Bild -** Kombinieren Sie mehrere Datenpunkte über all Ihre Content-Distributoren hinweg, um einen vollständigen Überblick über Ihre gesamte Medienaktivität zu erhalten und mithilfe der Funktion " [Federated Analytics](data-sharing/federated-analytics.md) "Interaktionen und Ansichten/Listening über alle möglichen Kanäle zu messen.
* **Umfangreiche Details:** Untersuchen Sie das Besucherverhalten so detailliert wie möglich, einschließlich der individuellen Besuchszeit, der gleichzeitigen Besucher pro Minute und der durchschnittlichen Wiedergabezeit von Inhalten.
* **Präzise Messung:** Untersuchen Sie verschiedenste Geräte zur Mediennutzung, einschließlich OTT, Smartphone, Tablet, Desktop und mehr, um Anwenderinteraktionen und Verhaltensmuster zu analysieren.
* **Segmentierung:** Wenden Sie auf Player, Geräte, Genres, Kapitel und Sendungen Klassifizierungen an, um herauszufinden, wie sie sich auf die Aufrufe und die Kundeninteraktion mit Inhalten und Anzeigen auswirken.

## Vorteile von Heartbeat gegenüber Milestone {#section_cnj_5st_p1b}

Adobe Analytics für Media lässt sich auf zwei Arten messen: die alte Milestone-Methode (nur Video) und die aktuelle Heartbeats-Methode (Audio und Video, sowohl im Media SDK als auch in der Media Collection-API verfügbar). Wir empfehlen für die Messung die Heartbeat-Methode und raten allen Kunden, diese Methode zu implementieren, sofern noch nicht geschehen, um die unten beschriebenen Vorteile nutzen zu können.

Die veraltete Meilenstein-Methode basiert auf individuellen Serveraufrufen des Analytics-Servers für Videostarts, -quartile, -dauer und-abschlüsse. Die Heartbeat-Methode bietet eine bessere Performance beim Medien-Tracking: Die Lösung misst den Hauptinhalt in 10-Sekunden-Intervallen, um aussagekräftige, standardisierte Metriken bereitzustellen. Darüber hinaus hat Adobe hier Verbesserungen gegenüber der Milestone-Methode implementiert, die einen optimierten und reibungslosen Implementierungsprozess über das von Heartbeats verwendete Medien-SDK bzw. die Mediensammlungs-API ermöglichen.

Zu den Vorteilen der Heartbeat-Methode zählen folgende Punkte:

* **Optimierter Implementierungsprozess:** Ordnen Sie Variablen über die Player-API einfacher zu und validieren Sie Implementierungen über das Adobe-Debugging-Tool, um sicherzustellen, dass alle erforderlichen Variablen richtig verfolgt werden.
* **Automatische Adobe Experience Cloud-Integration:** Nutzen Sie die automatische Integration in die Adobe Experience Cloud mithilfe der Experience Cloud ID, segmentieren Sie Ihre Medienzielgruppen, sprechen Sie sie gezielt an und stellen Sie basierend auf Anwendervorlieben Medienempfehlungen bereit.
* **Kombinierte Daten dank Federated Analytics:** Nutzen Sie unsere branchenweit ersten Funktionen zur Weitergabe von Mediendaten, um die Daten ganzheitlich über all Ihre Distributionspartner (Betreiber, Programmersteller und Distributoren) zu evaluieren.
* **Partnerschaften mit zertifizierten Partnern zur Bewertung:** Adobe arbeitet mit dem Zielgruppenbewertungsexperten Nielsen zusammen, um neutrale, vertrauenswürdige und zertifizierte Drittanbietermessungen bereitzustellen.
* **Standardisierte Lösung für alle Plattformen:** Nutzen Sie über alle Medienplattformen hinweg einheitliche und standardisierte Variablen, um effizientere Vergleiche zwischen Kampagnen, Geräten und Anbietern zu ermöglichen.

### Vergleichstabelle

|  | Video Analytics – Milestone | Media Analytics – Heartbeats  |
|---|---|---|
| **Medienereignisse** | Übergeordnete Standardereignisse | Ausführliche und anwenderspezifische Ereignisse für Hauptinhalt alle 10 Sekunden, für Anzeigen jede Sekunde |
| **Metriken und Dimensionen** | Abweichungen zwischen Anbietern, nicht standardisierte Metriken und Dimensionen | Klare, standardisierte Metriken, Dimensionen und Benchmarks über Anbieter hinweg |
| **Integrationen in Adobe-Produkte** | Individuelle Sitzungen mit einigen Zuordnungen und Integrationen | Kombinierte Experience Cloud ID, die für die einfachere übergreifende Analyse mit der vollständigen Adobe Experience Cloud verknüpft ist |
| **Preise** | Bei jedem Server-Aufruf verfolgt und abgerechnet | Transparentes Tracking nach Medien-Stream (einzeln) |
| **Implementierung und Support** | Längere Integrationen mit eingeschränktem Support bei Legacy-Versionen und ohne Upgrades | Optimierte Konfiguration mit laufenden Updates und Verbesserungen |
| **Weitergabe an Partner** | – | Federated Analytics und zertifizierte Metriken |
| **Erweitertes Tracking** | – | Tracking von Fehlerbehebungen und gleichzeitigen Zuschauern |

## Unterstützte Geräte {#section_lkm_l5t_p1b}

Adobe Analytics for Media hat sich mit der Branche weiterentwickelt und bietet leistungsstarke Datensammlungstools, um zu gewährleisten, dass jeder Medien-Stream erfasst wird und über alle wichtigen Geräte hinweg zu Berichten hinzugefügt werden kann. Unser Medien-SDK wurde für die am häufigsten verwendeten Geräte entwickelt, darunter:

* iOS- und Android-Smartphones und -Tablets
* OTT-Geräte für Roku, Apple TV, FireTV und Android TV
* JavaScript-Browser für Desktop und Laptop

Die SDKs werden regelmäßig aktualisiert, wenn neue Versionen der Geräte veröffentlicht werden. Diese SDKs ermöglichen die Integration mit den meisten großen Medienplayern, einschließlich Brightcove und Ooyala.

Bei Geräten oder Plattformen, die das SDK derzeit nicht unterstützt oder für die Sie es nicht verwenden wollen, können Sie die Mediensammlungs-API implementieren, über die Sie RESTful API-Aufrufe direkt vom Gerät/von der Plattform an das Media Analytics-Backend senden können.

Die unten stehende Tabelle enthält eine Liste der Geräte, die aktuell über die Medien-SDK-Implementierung bzw. Implementierung der Mediensammlungs-API unterstützt werden. Hier können Sie die neueste Version des SDK herunterladen: [SDKs herunterladen.](sdk-implement/download-sdks.md) Wenn ein Gerät nicht aufgeführt ist, das Sie messen möchten, erfragen Sie den Gerätestatus beim Kundendienst oder bei Ihrem Lösungsberater.

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

Weitere Informationen zu Media SDK finden Sie unter Unterstützung für [Plattformversionen.](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Sicherheit der Transportebene {#transport-layer-security}

**TLS Notice —** Adobe verfügt über Sicherheitsstandards, die das Ende der Lebensdauer älterer Sicherheitsprotokolle erfordern. Um weiterhin die sich entwickelnden Sicherheitsprotokollstandards zu erfüllen, entwickelt Adobe den Einsatz von TLS 1.2, um die aktuellste und sicherste Version zu verwenden. Ab dem 20. Februar 2019 unterstützt Adobe nur TLS 1.1 oder höher. Mit dieser Änderung erfasst Adobe keine Daten mehr von Endbenutzern mit älteren Geräten oder Webbrowsern, die TLS 1.0 bereitstellen. Die Migration auf TLS 1.2 bietet eine verbesserte Sicherheit. Für einen reibungslosen Übergang sollten Sie die Details zu diesem Thema genau durchlesen und die Änderungen entsprechend planen.

>[!NOTE]
>
>TLS ist derzeit das am häufigsten verwendete Sicherheitsprotokoll, das in Webbrowsern und anderen Anwendungen verwendet wird, bei denen Daten sicher über ein Netzwerk ausgetauscht werden müssen.
