---
seo-title: Voraussetzungen
title: Voraussetzungen
uuid: 4 c 0 b 37 f 3-8615-4 cc 0-b 9 c 9-eeb 290067064
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# Voraussetzungen{#prerequisites}

## Decisions {#decision}

Bevor Sie mit der Tracking-Implementierung beginnen, müssen Sie einige Entscheidungen bezüglich der optimalen Implementierung für Ihre Situation treffen:

* **Media Analytics:** Verwendung der neuesten Medien-SDKs (Standard, empfohlene Implementierung) und/oder der Mediensammlungs-API (RESTful)
* **Milestone:** Die ältere Adobe Tracking-Implementierung
* **Dateneinfügungs-APIs:** Implementierung von Tracking ohne Verwendung von Medien-SDKs

## Aufgaben {#prereq-tasks}

For a *Media Analytics* implementation, here are the tasks you must complete before you begin:

1. **Aktivieren Sie die Experience Cloud.**

   Sie müssen den Adobe Experience Platform Identity Service implementieren.

   Der Identitätsdienst aktiviert das allgemeine Identifizierungsframework für die Experience Cloud Core Services, Lösungen und Kundenattribute und Zielgruppen im Core-Core-Service von Personen. Es funktioniert durch die Zuweisung einer eindeutigen, dauerhaften ID zu einem Sitebesucher. Wenn Ihre Organisation den ID-Dienst implementiert, können Sie mit dieser ID denselben Site-Besucher und seine Daten in unterschiedlichen Experience Cloud-Lösungen identifizieren.

   ![](assets/mc_id_service_graphic.png)

   Der ID-Dienst kann auch die unterschiedlichen lösungsspezifischen IDs (z. B. die Analytics-AID) ersetzen. Über [Kunden-IDs und Authentifizierungsstatus](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html) ermöglicht es Ihnen der ID-Dienst, eigene Kunden-IDs an Experience Cloud zu übergeben. Beachten Sie jedoch, dass der ID-Dienst nur mit den Lösungen funktioniert, die Sie bereits abonniert haben. Wenn Sie nicht für andere Produkte angemeldet sind, gewährt der ID-Dienst keinen Zugriff.

   Künftig ist der ID-Dienst eine integrale Komponente von vielen aktuellen und künftigen Experience Cloud-Features, -Erweiterungen und -Services. Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Zur Teilnahme an der Adobe Experience Cloud Device Kooperation ist der Experience Cloud ID-Dienst erforderlich.

   Wenn Sie den ID-Dienst nicht implementiert haben, ist es nun an der Zeit, eine Migrationsstrategie in Erwägung zu ziehen. For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Aktivieren Sie die Adobe Analytics-Berichte.**

   Um Berichte in Analytics zu aktivieren und die erfassten Inhalts- und Anzeigendaten anzuzeigen, lesen Sie den Abschnitt [Aktivierung von Medienberichten.](../media-reports/media-reports-enable.md)

