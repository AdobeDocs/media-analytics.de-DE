---
title: Informationen zu den Voraussetzungen für Streaming-Medien
description: Erste Schritte mit Adobe Analytics Streaming Media. Erfahren Sie, was Sie zur Implementierung von Adobe Analytics für Streaming-Medien benötigen.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 50%

---

# Voraussetzungen {#prerequisites}

Führen Sie die folgenden Aufgaben aus, um Adobe Analytics für Streaming-Medien zu implementieren:

1. **Ihr Preismodell für Streaming-Medien bestätigen**<br>
Das aktuelle Preismodell basiert auf Video-Streams. Wenden Sie sich bei Bedarf an Ihren Kundenbetreuer oder Kundenbetreuer, um einen neuen Kundenauftrag zu unterzeichnen, da Streaming Media Analytics separat von Adobe Analytics verkauft wird.

1. **Überprüfen Sie, ob Sie Adobe Analytics implementieren**<br>
Streaming-Medien für Adobe Analytics erfordern auch eine grundlegende Implementierung der Adobe Analytics. Siehe [Implementieren von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) für weitere Informationen.

1. **Abrufen der Medien-Tracking-Server-URL**<br>
Fragen Sie Ihren Adobe Analytics-Support-Mitarbeiter nach der URL des Medien-Tracking-Servers. Dies ist die 
`collection-api-server` URL für das Mobile SDK, das JavaScript-SDK und den Tracking-Server ohne Sammlungs-API für Roku. Domänennamen für die API-Implementierung sind: `[your_namespace].hb-api.omtrdc.net`.

1. **Laden Sie das aktuelle Media SDK herunter oder implementieren Sie die erforderlichen Erweiterungen**<br>
Abhängig vom Implementierungspfad [das aktuelle SDK herunterladen](download-sdks.md) für Web-, mobile oder übergeordnete Plattformen. Die erforderlichen Erweiterungen müssen implementiert werden, um Adobe Analytics für Streaming-Medien zu aktivieren. Informationen zu erforderlichen Erweiterungen finden Sie unter [Adobe-Erweiterungen](download-sdks.md#media-extension). (Erforderlich, um entweder das Medien-SDK herunterzuladen oder die Erweiterung abzurufen)

1. **Aktivieren von Adobe Analytics-Berichten**<br>
Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, müssen Sie Berichte in Analytics aktivieren. Siehe [Aktivierung von Medienberichten.](/help/reporting/media-reports-enable.md).

1. **Aktivieren Sie die Experience Cloud**<br>


## Implementieren von Adobe Experience Platform Identity Service. {#implement-id}

Die **Identity Service** ermöglicht das allgemeine Identifizierungs-Framework für die Experience Cloud Core Services, Lösungen sowie Kundenattribute und Zielgruppen im People-Hauptdienst. Der ID-Dienst funktioniert durch die Zuweisung einer eindeutigen, dauerhaften ID zu einem Site-Besucher. Wenn Ihr Unternehmen den ID-Dienst implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in unterschiedlichen Experience Cloud-Lösungen identifizieren.

![ID-Dienst-Grafik](assets/mc_id_service_graphic.png)

Der ID-Dienst kann auch die verschiedenen lösungsspezifischen IDs ersetzen (z. B. Analytics AID). Mit der Funktion [Kunden-IDs und Authentifizierungsstatus](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=de) ermöglicht es Ihnen der ID-Dienst, eigene Kunden-IDs an Experience Cloud zu übergeben. Beachten Sie jedoch, dass der ID-Dienst nur mit den Lösungen funktioniert, für die Sie bereits ein Abonnement abgeschlossen haben. Wenn Sie nicht für den Zugriff auf andere Produkte angemeldet sind, bietet der ID-Dienst keinen Zugriff.

Der ID-Dienst ist eine integrale Komponente von vielen Experience Cloud-Funktionen, -Erweiterungen und -Services. Der ID-Dienst unterstützt derzeit [Analytics,](https://www.adobe.com/de/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/de/marketing-cloud/data-management-platform.html) und [Target.](https://www.adobe.com/de/marketing-cloud/testing-targeting.html)

Wenn Sie den ID-Dienst nicht implementiert haben, ist es nun an der Zeit, eine Migrationsstrategie in Erwägung zu ziehen. Weitere Informationen über die Bedeutung und die Rolle des ID-Dienstes finden Sie unter [Warum Sie den ID-Dienst im Auge behalten sollten.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

Weitere Informationen zur Experience Cloud-ID finden Sie unter [Überblick über die Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) und unter [Adobe Experience Platform-ID-Dienst](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).
