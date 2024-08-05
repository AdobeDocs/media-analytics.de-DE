---
title: Federated Media
description: Der Federated Media-Dienst bietet ein System zur Freigabe von Streaming-Mediendaten zwischen zwei Partnern.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0079116bcf39bb6d20b4fd5f14bd3c19137c46e3
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 60%

---

# Federated Media{#federated-media}

Der Federated Media-Dienst bietet ein System zur Freigabe von Streaming-Mediendaten (Audio und Video) zwischen zwei Partnern.
Die vom Streaming-Mediensammlungs-Add-on erstellten standardisierten Messdaten sind das Markenzeichen für Federated Media, sodass dieselben Daten aus mehreren Quellen in einen einzigen Bericht fließen können.
Über die Regeln und Logik von Federated Media lassen sich Daten einfach kontrollieren und individuell an die Bedürfnisse jeder Partnerschaft anpassen.
Federated Media sorgt für eine effizientere, optimierte und umsetzbare Audio- und Videomessung.

## Vorteile {#benefits}

* **Transparent:** Die Datenerstellung ist erkennbar. Für alle Firmen wird die gleiche Logik verwendet.
* **Umfassend:** Sie sind über die volle Reichweite und Auswirkung des Audio- und Videokonsums bei allen Partnerschaften, Plattformen und Geräten informiert.
* **Sicher:** Die Datenfreigabe kann Server-seitig mithilfe von Regeln und Logik gesteuert werden.
* **Standardisiert:** Sie sprechen dieselbe Datensprache wie Ihre Partner.
* **Umsetzbar:** Sie können Audio- und Videodaten quantifizieren, um Player zu bewerten, Trends zu überwachen und Anomalien mithilfe von Adobe Analytics zu erkennen.
* **Zentralisiert:** Sie erfassen Audio- und Videomessungsdaten in einem zentralen Adobe-System
* **Gesetzeskonform:** Sie erfüllen die gesetzlichen Datenfreigabe-Anforderungen.
* **Aktuell:** Sie senden und empfangen Daten nahezu in Echtzeit.
* **Einfach:** Wenn Sie Player einmal mit Adobe-SDKs getaggt haben, können Sie Daten mit vielen Partnern teilen.

## Definitionen {#definitions}

* **Sender:** Kunde, der Audio- und Videoanalysedaten auf eigenen Playern generiert
* **Empfänger:** Kunde, der Audio- und Videoanalysedaten vom Sender erhält

## Voraussetzungen {#requirements}

* **Medien-Stream-Vertrag:** Empfänger und Sender müssen über einen Adobe Analytics-Vertrag für Medien-Streams verfügen, bevor sie auf Audio- und Videodaten in Adobe Analytics zugreifen können. Weitere Informationen erhalten Sie von Ihrem Konto-Team.
* **Federated-Vertragszusatz:** Jeder Sender und Empfänger muss über einen unterzeichneten Vertragszusatz mit Adobe verfügen, bevor Daten gesendet oder empfangen werden können. Ein Vertragszusatz pro Kunde ist erforderlich, nicht ein Vertragszusatz pro Partnerschaft. Weitere Informationen erhalten Sie von Ihrem Konto-Team.

* **Implementierung des Add-ons für Streaming-Mediensammlung:** Der Sender muss das Add-on für Streaming-Mediensammlung auf allen Playern implementieren, die Teil des zusammengeführten Datensatzes sein werden. Nur Streaming-Mediendaten stehen zum Verknüpfen zur Verfügung. Weitere Informationen finden Sie unter [Übersicht über das Adobe Streaming Media Collection Add-on](/help/media-overview.md).

* **Adobe-Consulting-Vertrag:** Für die Ersteinrichtung der Föderierungsregeln zwischen Empfänger und Sender stehen Ihnen hilfreiche Beratungsservices zur Datenüberprüfung und zur Erstellung der Datenweitergabe-Vereinbarung zur Verfügung.

## Federated Media-Formular herunterladen

Laden Sie das Formular [Vereinbarung über die Föderierungsregeln](assets/federated_analytics_form.pdf) herunter und füllen Sie es aus, um an Federated Media teilzunehmen.

## Prozess {#process}

1. Sender und Empfänger arbeiten zusammen, um das Formular der Vereinbarung zu Föderierungsregeln auszufüllen. Das Formular zur Vereinbarung über die Verknüpfungsregeln enthält spezielle Felder für unser Engineering-Team und sollte NUR mit Adobe Acrobat bearbeitet werden. [Acrobat können Sie hier kostenlos herunterladen.](https://get.adobe.com/de/reader/)
1. Der Beratungsdienst stellt dem Empfänger eine Beispieldatendatei mit den tatsächlichen Daten von Sender-Playern zur Verfügung, damit korrekte Regeln für die Datenfreigabe definiert werden können, sofern Datendateien verfügbar sind.
1. Der Sender und der Empfänger stellen sicher, dass die Datenfreigabe-Vereinbarung alle vertraglichen Bedingungen zwischen den beiden Parteien erfüllt.
1. Der Beratungsdienst sendet das ausgefüllte Formular an Adobe Engineering, um Regeln für die Datenfreigabe einzurichten.
1. Die Daten werden für die Entwicklung der Adobe Analytics Report Suite oder des Adobe Experience Platform-Datenspeichers freigegeben, in dem der Empfänger Daten überprüft und validiert.
1. Sobald der Empfänger bestätigt hat, dass die Daten korrekt sind, aktualisiert Adobe Engineering die Regeln, um auf eine Analytics-Produktions-Report Suite oder einen Adobe Experience Platform-Datastream zu verweisen.
1. Der Empfänger überprüft und validiert Daten in der Produktions-Analytics Report Suite oder im Adobe Experience Platform-Datastream.
1. Wenn sich in Zukunft Änderungen am Datensatz ergeben, kann der Sender oder Empfänger ein Kundenunterstützungs-Ticket für den Support eröffnen.
