---
title: Informationen zu den Voraussetzungen für Streaming-Medien
description: Erste Schritte mit Adobe Analytics Streaming Media. Erfahren Sie, was Sie zur Implementierung von Adobe Analytics für Streaming-Medien benötigen.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 100%

---

# Voraussetzungen {#prerequisites}

## Entscheidungen {#decision}

Bevor Sie mit der Implementierung des Trackings beginnen, müssen Sie auswählen, welche Implementierung für Ihre Situation am sinnvollsten ist:

* **Medienanalyse -** Verwenden der neuesten Media SDKs (die standardmäßige, empfohlene Implementierung) und/oder der Media Collection API (RESTful)
* **Milestone -** Die ältere Adobe-Tracking-Implementierung
* **Data Insertion APIs -** Tracking-Implementierung ohne Verwendung von Media SDKs

## Aufgaben {#prereq-tasks}

Für eine Implementierung von *Media Analytics* müssen Sie die folgenden Aufgaben ausführen, bevor Sie beginnen:

1. **Aktivieren Sie die Experience Cloud.**

   Implementieren Sie den ID-Dienst für Adobe Experience Platform.

   Mit dem ID-Dienst wird das allgemeine Identifizierungs-Framework für die Experience Cloud-Hauptdienste, Lösungen sowie Kundenattribute und Zielgruppen im Personen-Hauptdienst ermöglicht. Der ID-Dienst funktioniert durch die Zuweisung einer eindeutigen, dauerhaften ID zu einem Site-Besucher. Wenn Ihr Unternehmen den ID-Dienst implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in unterschiedlichen Experience Cloud-Lösungen identifizieren.

   ![](assets/mc_id_service_graphic.png)

   Der ID-Dienst kann auch die verschiedenen lösungsspezifischen IDs ersetzen (z. B. Analytics AID). Mit der Funktion [Kunden-IDs und Authentifizierungsstatus](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=de) ermöglicht es Ihnen der ID-Dienst, eigene Kunden-IDs an Experience Cloud zu übergeben. Beachten Sie jedoch, dass der ID-Dienst nur mit den Lösungen funktioniert, für die Sie bereits ein Abonnement abgeschlossen haben. Wenn Sie nicht für den Zugriff auf andere Produkte angemeldet sind, bietet der ID-Dienst keinen Zugriff.

   Der ID-Dienst wird in Zukunft eine integrale Komponente von vielen aktuellen und künftigen Experience Cloud-Features, -Erweiterungen und -Services sein. Der ID-Dienst unterstützt derzeit [Analytics,](https://www.adobe.com/de/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/de/marketing-cloud/data-management-platform.html) und [Target.](https://www.adobe.com/de/marketing-cloud/testing-targeting.html)

   Wenn Sie den ID-Dienst nicht implementiert haben, ist es nun an der Zeit, eine Migrationsstrategie in Erwägung zu ziehen. Weitere Informationen über die Bedeutung und die Rolle des ID-Dienstes finden Sie unter [Warum Sie den ID-Dienst im Auge behalten sollten.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Weitere Informationen zur Experience Cloud-ID finden Sie unter [Überblick über die Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) und unter [Adobe Experience Platform-ID-Dienst](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).

1. **Aktivieren Sie die Adobe Analytics-Berichte.**

   Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, lesen Sie den Abschnitt [Aktivierung von Medienberichten.](/help/media-reports/media-reports-enable.md)
