---
title: Erste Schritte
description: Erste Schritte mit Adobe Analytics für Streaming-Medien.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 6%

---

# Erste Schritte {#getting-started}

Adobe Analytics for Streaming Media bietet zwei Hauptimplementierungsmethoden: die Medien-SDKs und die Mediensammlungs-APIs.

![methods](assets/getting-started2.png)

Verwenden der integrierten Logik der **Medien-SDKs** können Sie mehrere Medienplattformen genau messen, darunter Websites, Mobiltelefone, angeschlossene TVs, Tablets, OTT-Geräte, Set-Top-Boxen und Spielekonsolen. Sie können sogar heruntergeladene Inhalte messen. Die Einblicke, die Sie erhalten, gehen tief in die Interaktion mit der Benutzeranzeige ein, sodass Sie verstehen können, wie lange, wann und wo die Betrachter interagieren. Die Medien-SDK verwenden die **Mediensammlungs-APIs** für Tracking. Die Mediensammlungs-APIs können angepasst werden, wenn Ihre Anwendung benutzerdefinierte Tracking-Funktionen erfordert. Für Geräte, die von den Media SDKs nicht unterstützt werden, können Sie die Mediensammlungs-APIs verwenden.

Die Adobe Analytics Streaming Media-Lösung ist für die folgenden Medienplattformen verfügbar:

* Web
* Mobile
* Nach oben
* Jedes verbundene Gerät, das für Streaming-Medien oder eine Server-zu-Server-Integration verwendet werden kann

Weitere Informationen finden Sie unter [Unterstützte Geräte und Plattformen](#_Supported_devices_and).

>[!IMPORTANT]
>
>Wenden Sie sich zur Implementierung von Adobe Analytics Streaming Media an Ihren Kundenbetreuer oder Kundenbetreuer, um sicherzustellen, dass Streaming Media Teil Ihres Produktportfolios ist.

## Medien-SDKs für Streaming-Medien {#media-sdks}

Media SDKs für Streaming-Medien sind für die Plattformen JavaScript, Android, iOS, tvOS, Chromecast und Roku verfügbar.

Informationen zum Herunterladen und Installieren von Media SDKs finden Sie unter [Abrufen von Medien-SDKs, Erweiterungen mithilfe von Tags und OTT-SDKs](/help/getting-started/download-sdks.md).


## Mediensammlungs-APIs {#media-collection-apis}

Die **Mediensammlungs-APIs** können Sie Ihre Medienanalyseimplementierung anpassen. Verwenden Sie die Mediensammlungs-APIs, um die Server der Adobe direkt aufzurufen und so fast jede Aktion auszuführen, die Sie mit den SDKs ausführen können. Passen Sie Ihre Datenerfassung an, um Berichte zu erstellen, die wichtige Fragen zu Ihren Streaming-Mediendaten untersuchen, Einblicke erhalten oder beantworten.

Informationen zur Verwendung der Mediensammlungs-APIs finden Sie unter [Dokumentation zur Steaming Media-API](/help/implementation/media-collection-api/mc-api-overview.md).

## Adobe-Erweiterungen {#adobe-extensions}

* Die [**Adobe Medien Analytics für Audio und Video - Erweiterung**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) (Media Analytics-Erweiterung) ist für iOS- und tvOS-Implementierungen erforderlich. Es bietet die Funktionalität zum Hinzufügen der Tracker-Instanz zu einer Tag-Site oder einem Projekt. Für die MA-Erweiterung sind auch die Analytics-Erweiterung und die Experience Cloud-ID-Erweiterung erforderlich.

* [Analytics-Erweiterung v1.6 oder höher](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)—Mit dieser Erweiterung können Sie die JavaScript-Bibliothek des Adobe Experience Platform Web SDK laden, um Daten an Adobe-Lösungen zu senden.

* [Experience Cloud-ID-Erweiterung](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)—Diese Erweiterung implementiert den Experience Cloud-ID-Dienst, der Besucher über alle Experience Cloud-Lösungen hinweg identifiziert. Der Experience Cloud-ID-Dienst ist eine Personalisierungserweiterung in Adobe Experience Platform.
