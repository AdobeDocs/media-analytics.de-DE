---
title: Informationen zu den Voraussetzungen für Streaming-Medien
description: Erste Schritte mit Adobe Analytics Streaming Media. Erfahren Sie, was Sie zur Implementierung von Adobe Analytics für Streaming-Medien benötigen.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 60702b2cf466df7a1b328743c5d5f4c1834d9554
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 75%

---

# Voraussetzungen  {#prerequisites}

Führen Sie vor der Implementierung von Streaming-Medien die folgenden Aufgaben aus:

1. **Übersicht über Streaming-Medien**<br>
Bevor Sie mit der Implementierung von Streaming-Medien beginnen, lesen Sie die [Übersicht über Streaming-Medien](/help/media-overview.md) , um sicherzustellen, dass die Streaming-Medien Ihren Anforderungen entsprechen.

1. **Bestätigen des Preismodells für Streaming-Medien**<br>
Das aktuelle Preismodell basiert auf Video-Streams. Wenden Sie sich bei Bedarf an Ihren Kundenbetreuer oder Ihr Adobe Account-Team, um einen neuen Kundenauftrag zu unterzeichnen, da Streaming Media Analytics separat von Adobe Analytics verkauft wird.

1. **Aktivieren von Adobe Analytics-Berichten**<br>
Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte in Analytics aktivieren. Siehe [Aktivierung von Medienberichten](/help/reporting/media-reports-enable.md).

1. **Implementieren des Adobe Experience Platform Identity-Diensts in Experience Cloud**

   Mit dem **Identity Service** wird das allgemeine Identifizierungs-Framework für die Core Services von Experience Cloud, Lösungen sowie Kundenattribute und Audiences im Coreservice für Personen ermöglicht. Der ID-Dienst funktioniert durch die Zuweisung einer eindeutigen, dauerhaften ID zu einem Site-Besucher. Wenn Ihr Unternehmen den ID-Dienst implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in unterschiedlichen Experience Cloud-Lösungen identifizieren.

   ![Grafik des ID-Services](assets/mc_id_service_graphic.png)

   Der ID-Dienst kann auch die verschiedenen lösungsspezifischen IDs ersetzen (z. B. Analytics AID). Mit der Funktion [Kunden-IDs und Authentifizierungsstatus](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=de) ermöglicht es Ihnen der ID-Dienst, eigene Kunden-IDs an Experience Cloud zu übergeben. Beachten Sie jedoch, dass der ID-Dienst nur mit den Lösungen funktioniert, für die Sie bereits ein Abonnement abgeschlossen haben. Wenn Sie nicht für den Zugriff auf andere Produkte angemeldet sind, bietet der ID-Dienst keinen Zugriff.

   Der ID-Service ist eine integrale Komponente vieler Funktionen, Erweiterungen und Services von Experience Cloud. Der ID-Service unterstützt derzeit [Analytics](https://www.adobe.com/de/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/de/marketing-cloud/data-management-platform.html) und [Target](https://www.adobe.com/de/marketing-cloud/testing-targeting.html).

   Wenn Sie den ID-Dienst nicht implementiert haben, ist es nun an der Zeit, eine Migrationsstrategie in Erwägung zu ziehen. Weitere Informationen über die Bedeutung und die Rolle des ID-Dienstes finden Sie unter [Warum Sie den ID-Dienst im Auge behalten sollten.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Weitere Informationen zur Experience Cloud-ID finden Sie unter [Überblick über die Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) und unter [Adobe Experience Platform-ID-Dienst](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).

1. **Zusätzliche Voraussetzungen für Ihre Implementierungsmethode anzeigen**

   Je nachdem, wie Sie Streaming-Medien implementieren möchten, sehen Sie sich die Voraussetzungen für eine der folgenden Implementierungsmethoden an:

   * [Voraussetzungen für reine Adobe Analytics-Implementierungen](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Voraussetzungen für Edge-Implementierungen](/help/implementation/edge/prerequisites-edge.md)
