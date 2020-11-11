---
title: Federated Analytics
description: Der Federated Analytics-Dienst bietet ein System zur Freigabe von Adobe Analytics für Streaming-Mediendaten zwischen zwei Partnern.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: tm+mt
source-git-commit: 82b38f7870b6f890aaa812de30fa2d02d4f3ba8a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 92%

---


# Federated Analytics {#federated-analytics}

Der Federated Analytics-Dienst stellt ein System zur Freigabe von Adobe Media Analytics-Daten (Audio und Video) zwischen zwei Partnern bereit.
Die von Media Analytics erstellten standardisierten Messdaten sind das Markenzeichen für Federated Analytics, so dass dieselben Daten aus mehreren Quellen in einen einzigen Bericht fließen können.
Über die Regeln und die Logik von Federated Analytics können die Daten einfach kontrolliert und individualisiert werden, um die Anforderungen der jeweiligen Partnerschaft zu erfüllen.
Federated Analytics sorgt für eine optimierte Audio- und Videomessung mit gesteigerter Effizienz und aussagekräftigeren Daten.

## Vorteile  {#benefits}

* **Transparent:** Die Datenerstellung ist erkennbar. Für alle Firmen wird die gleiche Logik verwendet.
* **Umfassend:** Sie sind über die volle Reichweite und Auswirkung des Audio- und Videokonsums bei allen Partnerschaften, Plattformen und Geräten informiert.
* **Sicher:** Die Datenfreigabe kann Server-seitig mithilfe von Regeln und Logik gesteuert werden.
* **Standardisiert:** Sie sprechen dieselbe Datensprache wie Ihre Partner.
* **Umsetzbar:** Sie können Audio- und Videodaten quantifizieren, um Player zu bewerten, Trends zu überwachen und Anomalien mithilfe von Adobe Analytics zu erkennen.
* **Zentralisiert:** Sie erfassen Audio- und Videomessungsdaten in einem zentralen Adobe-System
* **Gesetzeskonform:** Sie erfüllen die gesetzlichen Datenfreigabe-Anforderungen.
* **Aktuell:** Sie senden und empfangen Daten nahezu in Echtzeit.
* **Einfach:** Wenn Sie Player einmal mit Adobe-SDKs getaggt haben, können Sie Daten mit vielen Partnern teilen.

## Definitionen  {#definitions}

* **Sender:** Kunde, der Audio- und Videoanalysedaten auf eigenen Playern generiert
* **Empfänger:** Kunde, der Audio- und Videoanalysedaten vom Sender erhält

## Voraussetzungen  {#requirements}

* **Medien-Stream-Vertrag:** Empfänger und Sender müssen über einen Adobe Analytics-Vertrag für Medien-Streams verfügen, bevor sie auf Audio- und Videodaten in Adobe Analytics zugreifen können. Weitere Informationen erhalten Sie von Ihrem Konto-Team.
* **Federated-Vertragszusatz:** Jeder Sender und Empfänger muss über einen unterzeichneten Vertragszusatz mit Adobe verfügen, bevor Daten gesendet oder empfangen werden können. Ein Vertragszusatz pro Kunde ist erforderlich, nicht ein Vertragszusatz pro Partnerschaft. Weitere Informationen erhalten Sie von Ihrem Konto-Team.

* **Implementierung von Media Analytics:** Der Sender muss Media Analytics auf allen Playern implementieren, die Teil des zusammengeführten Datensatzes sein werden. Es können nur Media Analytics-Daten zusammengeführt werden. Siehe Dokumentation: [Messen von Streaming-Medien in Adobe Analytics](/help/media-overview.md)

* **Adobe-Consulting-Vertrag:** Für die Ersteinrichtung der Föderierungsregeln zwischen Empfänger und Sender stehen Ihnen hilfreiche Beratungsservices zur Datenüberprüfung und zur Erstellung der Datenweitergabe-Vereinbarung zur Verfügung.

## Herunterladen des Federated Analytics-Formulars

Um an Federated Analytics teilzunehmen, laden Sie das [Federation Rules Agreement](federated-analytics-form.pdf)-Formular herunter und füllen Sie es aus.


## Verarbeitung {#process}

1. Sender und Empfänger arbeiten zusammen, um das Formular der Vereinbarung zu Föderierungsregeln auszufüllen. Das Formular zur Vereinbarung über die Verknüpfungsregeln enthält spezielle Felder für unser Engineering-Team und sollte NUR mit Adobe Acrobat bearbeitet werden. [Acrobat können Sie hier kostenlos herunterladen.](https://get.adobe.com/de/reader/)
1. Der Beratungsdienst stellt dem Empfänger eine Beispieldatendatei mit den tatsächlichen Daten von Sender-Playern zur Verfügung, damit korrekte Regeln für die Datenfreigabe definiert werden können, sofern Datendateien verfügbar sind.
1. Der Sender und der Empfänger stellen sicher, dass die Datenfreigabe-Vereinbarung alle vertraglichen Bedingungen zwischen den beiden Parteien erfüllt.
1. Der Beratungsdienst sendet das ausgefüllte Formular an Adobe Engineering, um Regeln für die Datenfreigabe einzurichten.
1. Die Daten werden für die Entwicklungs-Report Suite freigegeben, in der der Empfänger Daten überprüfen und validieren muss.
1. Sobald der Empfänger bestätigt hat, dass die Daten korrekt sind, aktualisiert Adobe Engineering die Regeln, damit diese auf eine Produktions-Report Suite verweisen.
1. Der Empfänger überprüft und validiert Daten in der Produktions-Report Suite.
1. Wenn sich in Zukunft Änderungen am Datensatz ergeben, kann der Sender oder Empfänger ein Kundenunterstützungs-Ticket für den Support eröffnen.
