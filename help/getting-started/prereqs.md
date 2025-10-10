---
title: Informationen zu den Voraussetzungen für Adobe Streaming Media Services
description: Erste Schritte mit den Services für Streaming-Medien. Erfahren Sie, was Sie für die Implementierung benötigen.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Streaming Media, Workspace Basics"
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 62%

---

# Voraussetzungen {#prerequisites}

Bevor Sie mit der Implementierung von Adobe Streaming Media Services beginnen, führen Sie die folgenden Aufgaben aus:

1. **Überblick über Adobe Streaming Media Services**<br>
Bevor Sie mit der Implementierung von Streaming Media Services beginnen, lesen Sie die [Übersicht über Adobe Streaming Media Services](/help/media-overview.md), um sicherzustellen, dass sie Ihren Anforderungen entspricht.

1. **Bestätigen Sie Ihr Preismodell**<br>
Das aktuelle Preismodell für das Add-on Customer Journey Analytics Streaming Media Collection und das Add-on Adobe Analytics for Streaming Media basiert auf Video-Streams. Wenden Sie sich bei Bedarf an Ihren Kundenbetreuer oder Ihr Adobe-Account-Team, da das Add-on separat für Adobe Analytics und Adobe Experience Platform erhältlich ist.

1. **Adobe Analytics-Berichte aktivieren**<br>
Um Berichte in Analytics oder Customer Journey Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte aktivieren. Siehe [Aktivierung von Medienberichten](/help/reporting/media-reports-enable.md).

1. **Implementieren des Adobe Experience Platform Identity Service in Experience Cloud**

   Mit dem **Identity Service** wird das allgemeine Identifizierungs-Framework für die Core Services von Experience Cloud, Lösungen sowie Kundenattribute und Zielgruppen im Coreservice für Personen ermöglicht. Der ID-Dienst funktioniert durch die Zuweisung einer eindeutigen, dauerhaften ID zu einem Site-Besucher. Wenn Ihr Unternehmen den ID-Dienst implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in unterschiedlichen Experience Cloud-Lösungen identifizieren.

   ![Grafik des ID-Services](assets/mc_id_service_graphic.png)

   Der ID-Dienst kann auch die verschiedenen lösungsspezifischen IDs ersetzen (z. B. Analytics AID). Mit der Funktion [Kunden-IDs und Authentifizierungsstatus](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=de) ermöglicht es Ihnen der ID-Dienst, eigene Kunden-IDs an Experience Cloud zu übergeben. Beachten Sie jedoch, dass der ID-Dienst nur mit den Lösungen funktioniert, für die Sie bereits ein Abonnement abgeschlossen haben. Wenn Sie nicht für den Zugriff auf andere Produkte angemeldet sind, bietet der ID-Dienst keinen Zugriff.

   Der ID-Service ist eine integrale Komponente vieler Funktionen, Erweiterungen und Services von Experience Cloud. Der ID-Service unterstützt derzeit [Analytics](https://www.adobe.com/de/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/de/marketing-cloud/data-management-platform.html) und [Target](https://www.adobe.com/de/marketing-cloud/testing-targeting.html).

   Wenn Sie den ID-Dienst nicht implementiert haben, ist es nun an der Zeit, eine Migrationsstrategie in Erwägung zu ziehen. Weitere Informationen über die Bedeutung und die Rolle des ID-Dienstes finden Sie unter [Warum Sie den ID-Dienst im Auge behalten sollten.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Weitere Informationen zur Experience Cloud-ID finden Sie unter [Überblick über die Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) und unter [Adobe Experience Platform-ID-Dienst](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).

1. **Anzeigen von zusätzlichen Voraussetzungen für Ihre Implementierungsmethode**

   Je nachdem, wie Sie Streaming-Medien-Services implementieren möchten, sehen Sie sich die Voraussetzungen für eine der folgenden Implementierungsmethoden an:

   * [Voraussetzungen für reine Adobe Analytics-Implementierungen](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Voraussetzungen für Edge-Implementierungen](/help/implementation/edge/prerequisites-edge.md)

   Verwenden Sie den [Implementierungsüberblick](/help/implementation/overview.md), um zu bestimmen, welche Implementierungsmethode für Sie geeignet ist.
